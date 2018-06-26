---
title: PathMeasure在项目中的使用
tags:
  - 自定义控件
  - PathMeasure
categories:
  - 自定义控件
date: 2018-6-10 12:18:15
---

### 控件预览
![](https://ws1.sinaimg.cn/large/5cc1a78ely1fsop2jaj42j20f10hatbw.jpg)
<!-- more -->
上面这个图片是最近项目中要实现的一个效果，圆弧是一个四分之一的半圆，很容易实现；但是黄色圆环部分有一部分是橘色的弧线，并且橘色弧线要和黄色圆环部分完全重合，其实如果通过改变画圆环的角度，也是可以画出橘色部分的弧线的，但是如果黄色的曲线不是圆环，而是贝塞尔曲线或者其他不规则曲线的话，要使得另外一段曲线完全和前面这段曲线某一部分完全重合的话，就需要使用PathMeasure来完成这个操作了。

### PathMeasure相关函数
1. setPath(Path path,boolean forceClosed)
    - 将Path和PathMeasure进行绑定.第一个参数是传入一个Path，代表我们需要进行测量的Path，第二个参数代表是否闭合，如果一段Path不是闭合的，但是forceClosed传true的话，就会按照闭合路径来测量这一段Path，比如计算路径长度就是计算的闭合的长度，但是path本身是没有这么长的。如果本来就是闭合path，这个参数就无所谓了。
2. getLength()
    - 计算Path的长度
3. getSegment(float startD, float stopD, Path dst, boolean startWithMoveTo)
    - 获取一段区间内的path，并生成一个新的对象，用dst来接收；第一个参数是起始长度，第二个参数是终止长度，第四个参数代表是否强制覆盖dst，如果设置为faslse，则每一次调用该方法，dst都会在已有path的基础上添加一段新path，如果设置为true，则dst会重新赋值，之前的path的值就都被覆盖了。
4. nextContour()
    - nextContour()方法用的比较少，比较大部分情况下都只会有一个Path而不是多个，毕竟这样会增加Path的复杂度，但是如果真有一个Path，包含了多个Path，那么通过nextContour这个方法，就可以进行切换，同时，默认的API，例如getLength，获取的也是当前的这段Path所对应的长度，而不是所有的Path的长度，同时，nextContour获取Path的顺序，与Path的添加顺序是相同的。
5. getPosTan (float distance, float[] pos, float[] tan)
    - 获取某个位置的坐标和正切值，分别赋值给pos和tan。

通过上面的几个方法，我们就能完成今天的demo了。

```java
public class CurveView extends View {

    private Paint mPaint;
    private PathMeasure mPathMeasure;
    private Path mPath;
    private Path destPath;
    private int strokeWidth;
    private Paint orangePaint;
    private float width;
    private float height;
    private float[] leftTop;
    private float[] rightBottom;
    private float[] rightTop;
    private float[] point1;
    private float[] point2;
    private float[] point3;
    private Paint pointPaint;
    private Paint jianTouPaint;
    private float[] pointCurrent;
    private float[] pointTarget;

    public CurveView(Context context) {
        super(context);
        initView();
    }

    public CurveView(Context context, @Nullable AttributeSet attrs) {
        super(context, attrs);
        initView();
    }

    public CurveView(Context context, @Nullable AttributeSet attrs, int defStyleAttr) {
        super(context, attrs, defStyleAttr);
        initView();
    }

    private void initView() {
        strokeWidth = DensityU.dip2px(getContext(), 15);
        mPaint = new Paint(Paint.ANTI_ALIAS_FLAG);
        mPaint.setColor(Color.parseColor("#ffe48a"));
        mPaint.setStrokeWidth(strokeWidth);
        mPaint.setStyle(Style.STROKE);
        mPaint.setStrokeCap(Cap.ROUND);


        jianTouPaint = new Paint(Paint.ANTI_ALIAS_FLAG);
        jianTouPaint.setColor(Color.parseColor("#ffe48a"));
        jianTouPaint.setStyle(Style.FILL_AND_STROKE);
        jianTouPaint.setStrokeWidth(DensityU.dip2px(getContext(), 4));
        jianTouPaint.setStrokeCap(Cap.ROUND);
        jianTouPaint.setStrokeJoin(Join.ROUND);

        orangePaint = new Paint(Paint.ANTI_ALIAS_FLAG);
        orangePaint.setColor(Color.parseColor("#ff7f00"));
        orangePaint.setStrokeCap(Cap.ROUND);
        orangePaint.setStrokeWidth(strokeWidth);
        orangePaint.setStyle(Style.STROKE);


        pointPaint = new Paint(Paint.ANTI_ALIAS_FLAG);
        pointPaint.setStyle(Style.STROKE);
        pointPaint.setStrokeWidth(strokeWidth);
        pointPaint.setStrokeCap(Cap.ROUND);
        pointPaint.setColor(Color.RED);
        mPathMeasure = new PathMeasure();
        mPath = new Path();
        destPath = new Path();
    }

    @Override protected void onSizeChanged(int w, int h, int oldw, int oldh) {
        super.onSizeChanged(w, h, oldw, oldh);
        width = w - DensityU.dip2px(getContext(), 36) + strokeWidth / 2f;
        height = h;


        leftTop = new float[]{-(width - strokeWidth / 2f), height - width - width + strokeWidth / 2f};
        rightBottom = new float[]{width - strokeWidth / 2f, height - strokeWidth / 2f};
        rightTop = new float[]{rightBottom[0], leftTop[1]};
        RectF rectF = new RectF(leftTop[0], leftTop[1], rightBottom[0], rightBottom[1]);
        mPath.addArc(rectF, 0, 88.4f);
        mPathMeasure.setPath(mPath, false);


        float length = mPathMeasure.getLength();
        point1 = new float[2];
        point2 = new float[2];
        point3 = new float[2];
        pointCurrent = new float[2];
        pointTarget = new float[2];
        //通过getPosTan方法，获取三个点的坐标，方便后面画小圆点
        mPathMeasure.getPosTan(0, point1, null);
        mPathMeasure.getPosTan(length / 9F * 2f, point2, null);
        mPathMeasure.getPosTan(length / 7F * 3f, point3, null);

        float currentLength = length - DensityU.dip2px(getContext(), 50);
        float targetLength = length - DensityU.dip2px(getContext(), 150);
        mPathMeasure.getPosTan(targetLength, pointTarget, null);
        mPathMeasure.getPosTan(currentLength, pointCurrent, null);

        //根据起点和终点位置的长度，生成新的Path.
        mPathMeasure.getSegment(targetLength, currentLength, destPath, true);
    }

    @Override protected void onMeasure(int widthMeasureSpec, int heightMeasureSpec) {
        int widthSpecSize = MeasureSpec.getSize(widthMeasureSpec);
        setMeasuredDimension(widthSpecSize, (int) (widthSpecSize + DensityU.dip2px(getContext(), 80)- DensityU.dip2px(getContext(), 36) + strokeWidth / 2f));
    }

    @Override protected void onDraw(Canvas canvas) {
        super.onDraw(canvas);
        canvas.drawPath(mPath, mPaint);


        canvas.drawPath(destPath, orangePaint);


        Path path = new Path();
        path.moveTo(rightTop[0], height - width + strokeWidth / 2f + 5);
        path.lineTo(rightTop[0], height - width + strokeWidth / 2f + 5 - DensityU.dip2px(getContext(), 60));


        canvas.drawPath(path, mPaint);
        path.reset();
        //绘制箭头
        path.moveTo(rightTop[0], height - width + strokeWidth / 2f + 8 - DensityU.dip2px(getContext(), 60));
        path.lineTo(rightTop[0] - DensityU.dip2px(getContext(), 32), height - width + strokeWidth / 2f - DensityU.dip2px(getContext(), 50));
        path.lineTo(rightTop[0], height - width + strokeWidth / 2f - DensityU.dip2px(getContext(), 80));
        path.lineTo(rightTop[0] + DensityU.dip2px(getContext(), 32), height - width + strokeWidth / 2f - DensityU.dip2px(getContext(), 50));
        path.close();
        canvas.drawPath(path, jianTouPaint);


        pointPaint.setColor(Color.parseColor("#FF4D30"));
        canvas.drawPoint(point1[0], point1[1], pointPaint);
        pointPaint.setColor(Color.parseColor("#70be1b"));
        canvas.drawPoint(point2[0], point2[1], pointPaint);
        pointPaint.setColor(Color.parseColor("#68a8f3"));
        canvas.drawPoint(point3[0], point3[1], pointPaint);
    }


    public float[] getPoint1() {
        return point1;
    }

    public float[] getPoint2() {
        return point2;
    }

    public float[] getPoint3() {
        return point3;
    }

    public float[] getPointCurrent() {
        return pointCurrent;
    }

    public float[] getPointTarget() {
        return pointTarget;
    }

    public int getStrokeWidth() {
        return strokeWidth;
    }
}

```
这样就完成了我们向上的抛物线箭头。
![](https://ws1.sinaimg.cn/large/5cc1a78ely1fsopmcun2hj20f40h9wfb.jpg)

控件中还有一些其他的元素，这时候就需要给他们定位了，通过PathMeasure的getPosTan方法，我们是可以获取到所有位置的坐标的。

```java
public class CurveLayout extends FrameLayout {
    public CurveLayout(Context context) {
        super(context);
        initView();
    }


    public CurveLayout(Context context, AttributeSet attrs) {
        super(context, attrs);
        initView();
    }

    public CurveLayout(Context context, AttributeSet attrs, int defStyleAttr) {
        super(context, attrs, defStyleAttr);
        initView();
    }


    private void initView() {
        LayoutInflater.from(getContext()).inflate(R.layout.curve_framelayout, this, true);
        final CurveView mCurveView = findViewById(R.id.curve_view);
        final RelativeLayout rlToefl = findViewById(R.id.rl_toefl);
        final RelativeLayout rlSenior = findViewById(R.id.rl_senior);
        final RelativeLayout rlJunior = findViewById(R.id.rl_junior);


        final LinearLayout llToefl = findViewById(R.id.ll_toefl);
        final LinearLayout llSenior = findViewById(R.id.ll_senior);
        final LinearLayout llJunior = findViewById(R.id.ll_junior);


        final LinearLayout llTarget = findViewById(R.id.ll_target);
        final FrameLayout flCurrent = findViewById(R.id.fl_current);

        final FrameLayout flCurrentText = findViewById(R.id.fl_current_text);

        mCurveView.post(new Runnable() {
            @Override public void run() {
                rlToefl.setTranslationY(mCurveView.getPoint1()[1] - DensityU.dip2px(getContext(), 30));
                rlSenior.setTranslationY(mCurveView.getPoint2()[1] - rlSenior.getHeight() + DensityU.dip2px(getContext(), 5));
                rlJunior.setTranslationY(mCurveView.getPoint3()[1] - rlJunior.getHeight() + DensityU.dip2px(getContext(), 5));

                llToefl.setTranslationY(mCurveView.getPoint1()[1] - DensityU.dip2px(getContext(), 10));
                llSenior.setTranslationY(mCurveView.getPoint2()[1] - DensityU.dip2px(getContext(), 10));
                llJunior.setTranslationY(mCurveView.getPoint3()[1] - DensityU.dip2px(getContext(), 10));

                rlToefl.setTranslationX(mCurveView.getPoint1()[0] - getWidth() - DensityU.dip2px(getContext(), 10));
                rlSenior.setTranslationX(mCurveView.getPoint2()[0] - getWidth() - DensityU.dip2px(getContext(), 10));
                rlJunior.setTranslationX(mCurveView.getPoint3()[0] - getWidth() - DensityU.dip2px(getContext(), 10));

                llToefl.setTranslationX(mCurveView.getPoint1()[0] + DensityU.dip2px(getContext(), 10));
                llSenior.setTranslationX(mCurveView.getPoint2()[0] + DensityU.dip2px(getContext(), 20));
                llJunior.setTranslationX(mCurveView.getPoint3()[0] + DensityU.dip2px(getContext(), 20));


                llTarget.setTranslationX(mCurveView.getPointTarget()[0] - llTarget.getWidth() / 2);
                llTarget.setTranslationY(mCurveView.getPointTarget()[1] - llTarget.getHeight() - DensityU.dip2px(getContext(), 8));

                flCurrent.setTranslationX(mCurveView.getPointCurrent()[0] - flCurrent.getWidth() / 2 - DensityU.dip2px(getContext(), 2));
                flCurrent.setTranslationY(mCurveView.getPointCurrent()[1] - flCurrent.getHeight() - DensityU.dip2px(getContext(), 3));


                flCurrentText.setTranslationX(mCurveView.getPointCurrent()[0] - flCurrent.getWidth() / 2 - DensityU.dip2px(getContext(), 2));
                flCurrentText.setTranslationY(mCurveView.getPointCurrent()[1] + DensityU.dip2px(getContext(), 13));
            }
        });
    }
}

```

下面是组合控件用到的一个布局：curve_framelayout

```html
<?xml version="1.0" encoding="utf-8"?>
<FrameLayout
    xmlns:android="http://schemas.android.com/apk/res/android"
    xmlns:app="http://schemas.android.com/apk/res-auto"
    xmlns:tools="http://schemas.android.com/tools"
    android:layout_width="match_parent"
    android:layout_height="match_parent"
    android:layout_marginLeft="10dp"
    tools:showIn="@layout/activity_main">

    <lieeber.com.guihua.CurveView
        android:id="@+id/curve_view"
        android:layout_width="match_parent"
        android:layout_height="wrap_content"
        android:layout_marginBottom="20dp"
        android:layout_marginRight="15dp"/>

    <RelativeLayout
        android:id="@+id/rl_toefl"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:layout_gravity="right">

        <TextView
            android:id="@+id/tv_toefl_num"
            android:layout_width="wrap_content"
            android:layout_height="wrap_content"
            android:text="8.8"
            android:textColor="#ff0000"
            android:textSize="30sp"/>

        <TextView
            android:layout_width="wrap_content"
            android:layout_height="wrap_content"
            android:layout_alignBottom="@+id/tv_toefl_num"
            android:layout_marginBottom="7dp"
            android:layout_toRightOf="@+id/tv_toefl_num"
            android:text="万小学生学到托福难度课程"
            android:textColor="#ff0000"
            android:textSize="14sp"
            android:textStyle="bold"/>

        <RelativeLayout
            android:layout_width="wrap_content"
            android:layout_height="wrap_content"
            android:layout_below="@+id/tv_toefl_num"
            android:gravity="center_vertical">

            <com.facebook.drawee.view.SimpleDraweeView
                android:id="@+id/iv_avatar"
                android:layout_width="40dp"
                android:layout_height="40dp"
                android:layout_marginRight="5dp"
                app:placeholderImage="@drawable/small_boy"
                app:roundAsCircle="true"/>

            <TextView
                android:id="@+id/tv_desc"
                android:layout_width="wrap_content"
                android:layout_height="wrap_content"
                android:layout_marginTop="8dp"
                android:layout_toRightOf="@+id/iv_avatar"
                android:text="六年级孩子与外教交流托福雅思难度话题"
                android:textColor="#000000"
                android:textSize="8sp"/>

            <TextView
                android:layout_width="wrap_content"
                android:layout_height="wrap_content"
                android:layout_below="@+id/tv_desc"
                android:layout_toRightOf="@+id/iv_avatar"
                android:text="成都泡桐树小学 六年级 牟天恒"
                android:textColor="#888888"
                android:textSize="7sp"/>
        </RelativeLayout>


    </RelativeLayout>


    <RelativeLayout
        android:id="@+id/rl_senior"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:layout_gravity="right"
        tools:layout_gravity="right|center_vertical">

        <TextView
            android:id="@+id/tv_senior_num"
            android:layout_width="wrap_content"
            android:layout_height="wrap_content"
            android:text="62"
            android:textColor="#FF000000"
            android:textSize="30sp"
            android:textStyle="bold"
            />

        <TextView
            android:layout_width="wrap_content"
            android:layout_height="wrap_content"
            android:layout_alignBottom="@+id/tv_senior_num"
            android:layout_marginBottom="7dp"
            android:layout_toRightOf="@+id/tv_senior_num"
            android:text="万小学生"
            android:textColor="#FF000000"
            android:textSize="10sp"
            android:textStyle="bold"/>

        <TextView
            android:layout_width="wrap_content"
            android:layout_height="wrap_content"
            android:layout_below="@+id/tv_senior_num"
            android:text="学到高中难度课程"
            android:textColor="#FF000000"
            android:textSize="11sp"
            android:textStyle="bold"/>
    </RelativeLayout>


    <RelativeLayout
        android:id="@+id/rl_junior"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:layout_gravity="right"
        tools:layout_gravity="right|bottom">

        <TextView
            android:id="@+id/tv_junior_num"
            android:layout_width="wrap_content"
            android:layout_height="wrap_content"
            android:text="218"
            android:textColor="#FF000000"
            android:textSize="30sp"
            android:textStyle="bold"
            />

        <TextView
            android:layout_width="wrap_content"
            android:layout_height="wrap_content"
            android:layout_alignBottom="@+id/tv_junior_num"
            android:layout_marginBottom="7dp"
            android:layout_toRightOf="@+id/tv_junior_num"
            android:text="万小学生"
            android:textColor="#FF000000"
            android:textSize="10sp"
            android:textStyle="bold"/>

        <TextView
            android:layout_width="wrap_content"
            android:layout_height="wrap_content"
            android:layout_below="@+id/tv_junior_num"
            android:text="学到初中难度课程"
            android:textColor="#FF000000"
            android:textSize="11sp"
            android:textStyle="bold"/>
    </RelativeLayout>


    <LinearLayout
        android:id="@+id/ll_toefl"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:layout_gravity="left"
        android:orientation="vertical"
        tools:layout_gravity="left">

        <ImageView
            android:layout_width="39dp"
            android:layout_height="24dp"
            android:layout_gravity="center_horizontal"
            android:scaleType="fitXY"
            android:src="@drawable/toefl_icon"/>

        <TextView
            android:layout_width="wrap_content"
            android:layout_height="wrap_content"
            android:layout_gravity="center_horizontal"
            android:text="托福"
            android:textColor="#000000"
            android:textSize="10sp"/>
    </LinearLayout>

    <LinearLayout
        android:id="@+id/ll_senior"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:layout_gravity="left"
        android:orientation="vertical"
        tools:layout_gravity="left|bottom">

        <ImageView
            android:layout_width="26dp"
            android:layout_height="28dp"
            android:layout_gravity="center_horizontal"
            android:scaleType="fitXY"
            android:src="@drawable/senior_icon"/>

        <TextView
            android:layout_width="wrap_content"
            android:layout_height="wrap_content"
            android:layout_gravity="center_horizontal"
            android:text="高中"
            android:textColor="#000000"
            android:textSize="10sp"/>
    </LinearLayout>

    <LinearLayout
        android:id="@+id/ll_junior"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:layout_gravity="left"
        android:orientation="vertical"
        tools:layout_gravity="left|center_vertical">

        <ImageView
            android:layout_width="30dp"
            android:layout_height="22dp"
            android:layout_gravity="center_horizontal"
            android:scaleType="fitXY"
            android:src="@drawable/junior_icon"/>

        <TextView
            android:layout_width="wrap_content"
            android:layout_height="wrap_content"
            android:layout_gravity="center_horizontal"
            android:text="初中"
            android:textColor="#000000"
            android:textSize="10sp"/>
    </LinearLayout>


    <LinearLayout
        android:id="@+id/ll_target"
        android:layout_width="44dp"
        android:layout_height="60dp"
        android:background="@drawable/drip_orange"
        android:gravity="center_horizontal"
        android:orientation="horizontal"
        android:paddingTop="9dp"
        tools:layout_marginTop="100dp">

        <TextView
            android:layout_width="wrap_content"
            android:layout_height="wrap_content"
            android:text="第"
            android:textColor="#ffffff"
            android:textSize="11sp"/>

        <TextView
            android:layout_width="wrap_content"
            android:layout_height="wrap_content"
            android:text="7"
            android:textColor="#ffffff"
            android:textSize="20sp"
            android:textStyle="bold"/>

        <TextView
            android:layout_width="wrap_content"
            android:layout_height="wrap_content"
            android:text="阶"
            android:textColor="#ffffff"
            android:textSize="11sp"/>
    </LinearLayout>


    <FrameLayout
        android:id="@+id/fl_current"
        android:layout_width="34dp"
        android:layout_height="46dp"
        android:background="@drawable/drip_yellow"
        tools:layout_marginTop="180dp">

        <com.facebook.drawee.view.SimpleDraweeView
            android:layout_width="30dp"
            android:layout_height="30dp"
            android:layout_gravity="center_horizontal"
            android:layout_marginTop="2dp"
            app:placeholderImage="@drawable/small_boy"/>
    </FrameLayout>


    <FrameLayout
        android:id="@+id/fl_current_text"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content">

        <TextView
            android:layout_width="wrap_content"
            android:layout_height="wrap_content"
            android:text="当前年级 三年级上"
            android:textColor="#000000"
            android:textSize="9sp"/>
    </FrameLayout>
</FrameLayout>
```

