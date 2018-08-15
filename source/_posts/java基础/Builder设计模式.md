---
title: 建造者模式
tags:
  - 设计模式
  - java
  - 建造者模式
categories:
  - java基础
date: 2018-6-11 12:18:15
---

### 概念
建造者模式是较为复杂的创建型模式，它将客户端与包含多个组成部分的复杂对象的创建过程分离，使得同样的构建过程可以创建不同的表示。

<!-- more -->

建造者模式包含以下几个核心模块

#### Builder（抽象建造者）

它为创建一个产品对象的各个部件指定抽象接口，在该接口中一般声明两类方法，一类方法是buildXXX()，它们用于创建复杂对象的各个部件；另一类方法是getXXX()，它们用于返回复杂对象。Builder既可以是抽象类，也可以是接口。

#### ConcreteBuilder（具体建造者）

它实现了Builder接口，实现各个部件的具体构造和装配方法，定义并明确它所创建的复杂对象，也可以提供一个方法返回创建好的复杂产品对象。

#### Product（产品角色）

它是被构建的复杂对象，包含多个组成部件，具体建造者ConcreteBuilder创建该产品的内部表示并定义它的装配过程。

#### Director（指挥者）

指挥者又称为导演类，它负责安排复杂对象的建造次序，指挥者与抽象建造者之间存在关联关系，可以在其construct()建造方法中调用建造者对象的部件构造与装配方法，完成复杂对象的建造。客户端一般只需要与指挥者进行交互，在客户端确定具体建造者的类型，并实例化具体建造者对象，然后通过指挥者类的构造函数或者Setter方法将该对象传入指挥者类中。

### 使用场景
当构造一个对象需要很多的参数，并且参数的个数或者类型不固定的时候，通过不同的参数组合，可以构建不同的对象，这时候我们就可以使用建造者模式。

下面是代码示例

```java 
/**
*抽象建造者
*/
public abstract class Builder {
    protected Product product = new Product();
    public abstract void buildPartA();
    public abstract void buildPartB();
    public abstract void buildPartC();

    public Product getProduct() {
        return product;
    }
}



/**
*具体建造者
*/
public class ConcreteBuilder extends Builder {
    @Override public void buildPartA() {
        product.setPartA("PartA");
    }

    @Override public void buildPartB() {
        product.setPartB("PartB");
    }

    @Override public void buildPartC() {
        product.setPartC("PartC");
    }
}


/**
*产品角色
*/
public class Product {
    private String partA;
    private String partB;
    private String partC;

    public void show() {
        System.out.println("Product{" +
                "partA='" + partA + '\'' +
                ", partB='" + partB + '\'' +
                ", partC='" + partC + '\'' +
                '}');
    }

    public String getPartA() {
        return partA;
    }

    public void setPartA(String partA) {
        this.partA = partA;
    }

    public String getPartB() {
        return partB;
    }

    public void setPartB(String partB) {
        this.partB = partB;
    }

    public String getPartC() {
        return partC;
    }

    public void setPartC(String partC) {
        this.partC = partC;
    }
}

/**
*指挥者
*/
public class Director {
    private Builder builder = new ConcreteBuilder();

    public Product productFirst() {
        builder.buildPartA();
        builder.buildPartC();
        return builder.getProduct();
    }

    public Product productSecond() {
        builder.buildPartB();
        builder.buildPartC();
        return builder.getProduct();
    }
}




public class Test {
    public static void main(String[] args) {
        Director director = new Director();
        Product productFirst = director.productFirst();
        Product productSecond = director.productSecond();
        productFirst.show();
        productSecond.show();
    }
}


```

从代码中可以看出，我们构建了produtFirst和productSecond两种产品，是通过partA，partB和partC不同的组合实现的。


### builder模式在Android中的实际运用：AlertDialog

AlertDialog的使用

```java 
 private void showDialog(Context context) {  
    AlertDialog.Builder builder = new AlertDialog.Builder(context);  
    builder.setIcon(R.drawable.icon);  
    builder.setTitle("Title");  
    builder.setMessage("Message");  
    builder.setPositiveButton("Button1",  
            new DialogInterface.OnClickListener() {  
                public void onClick(DialogInterface dialog, int whichButton) {  
                    setTitle("点击了对话框上的Button1");  
                }  
            });  
    builder.setNeutralButton("Button2",  
            new DialogInterface.OnClickListener() {  
                public void onClick(DialogInterface dialog, int whichButton) {  
                    setTitle("点击了对话框上的Button2");  
                }  
            });  
    builder.setNegativeButton("Button3",  
            new DialogInterface.OnClickListener() {  
                public void onClick(DialogInterface dialog, int whichButton) {  
                    setTitle("点击了对话框上的Button3");  
                }  
            });  
    builder.create().show();  // 构建AlertDialog， 并且显示
} 
    
```

AlertDialog的源码
```java 

// AlertDialog
public class AlertDialog extends Dialog implements DialogInterface {
    // Controller, 接受Builder成员变量P中的各个参数
    private AlertController mAlert;
 
    // 构造函数
    protected AlertDialog(Context context, int theme) {
        this(context, theme, true);
    }
 
    // 4 : 构造AlertDialog
    AlertDialog(Context context, int theme, boolean createContextWrapper) {
        super(context, resolveDialogTheme(context, theme), createContextWrapper);
        mWindow.alwaysReadCloseOnTouchAttr();
        mAlert = new AlertController(getContext(), this, getWindow());
    }
 
    // 实际上调用的是mAlert的setTitle方法
    @Override
    public void setTitle(CharSequence title) {
        super.setTitle(title);
        mAlert.setTitle(title);
    }
 
    // 实际上调用的是mAlert的setCustomTitle方法
    public void setCustomTitle(View customTitleView) {
        mAlert.setCustomTitle(customTitleView);
    }
    
    public void setMessage(CharSequence message) {
        mAlert.setMessage(message);
    }
 
    // AlertDialog其他的代码省略
    
    // ************  Builder为AlertDialog的内部类   *******************
    public static class Builder {
        // 1 : 存储AlertDialog的各个参数, 例如title, message, icon等.
        private final AlertController.AlertParams P;
        // 属性省略
        
        /**
         * Constructor using a context for this builder and the {@link AlertDialog} it creates.
         */
        public Builder(Context context) {
            this(context, resolveDialogTheme(context, 0));
        }
 
 
        public Builder(Context context, int theme) {
            P = new AlertController.AlertParams(new ContextThemeWrapper(
                    context, resolveDialogTheme(context, theme)));
            mTheme = theme;
        }
        
        // Builder的其他代码省略 ......
 
        // 2 : 设置各种参数
        public Builder setTitle(CharSequence title) {
            P.mTitle = title;
            return this;
        }
        
        
        public Builder setMessage(CharSequence message) {
            P.mMessage = message;
            return this;
        }
 
        public Builder setIcon(int iconId) {
            P.mIconId = iconId;
            return this;
        }
        
        public Builder setPositiveButton(CharSequence text, final OnClickListener listener) {
            P.mPositiveButtonText = text;
            P.mPositiveButtonListener = listener;
            return this;
        }
        
        
        public Builder setView(View view) {
            P.mView = view;
            P.mViewSpacingSpecified = false;
            return this;
        }
        
        // 3 : 构建AlertDialog, 传递参数
        public AlertDialog create() {
            // 调用new AlertDialog构造对象， 并且将参数传递个体AlertDialog 
            final AlertDialog dialog = new AlertDialog(P.mContext, mTheme, false);
            // 5 : 将P中的参数应用的dialog中的mAlert对象中
            P.apply(dialog.mAlert);
            dialog.setCancelable(P.mCancelable);
            if (P.mCancelable) {
                dialog.setCanceledOnTouchOutside(true);
            }
            dialog.setOnCancelListener(P.mOnCancelListener);
            if (P.mOnKeyListener != null) {
                dialog.setOnKeyListener(P.mOnKeyListener);
            }
            return dialog;
        }
    }
    
}

```
可以看到，通过Builder来设置AlertDialog中的title, message, button等参数，这些参数都存储在类型为AlertController.AlertParams的成员变量P中，AlertController.AlertParams中包含了与之对应的成员变量。在调用Builder类的create函数时才创建AlertDialog, 并且将Builder成员变量P中保存的参数应用到AlertDialog的mAlert对象中，即P.apply(dialog.mAlert)代码段。我们看看apply函数的实现 : 

```java 
public void apply(AlertController dialog) {
    if (mCustomTitleView != null) {
        dialog.setCustomTitle(mCustomTitleView);
    } else {
        if (mTitle != null) {
            dialog.setTitle(mTitle);
        }
        if (mIcon != null) {
            dialog.setIcon(mIcon);
        }
        if (mIconId >= 0) {
            dialog.setIcon(mIconId);
        }
        if (mIconAttrId > 0) {
            dialog.setIcon(dialog.getIconAttributeResId(mIconAttrId));
        }
    }
    if (mMessage != null) {
        dialog.setMessage(mMessage);
    }
    if (mPositiveButtonText != null) {
        dialog.setButton(DialogInterface.BUTTON_POSITIVE, mPositiveButtonText,
                mPositiveButtonListener, null);
    }
    if (mNegativeButtonText != null) {
        dialog.setButton(DialogInterface.BUTTON_NEGATIVE, mNegativeButtonText,
                mNegativeButtonListener, null);
    }
    if (mNeutralButtonText != null) {
        dialog.setButton(DialogInterface.BUTTON_NEUTRAL, mNeutralButtonText,
                mNeutralButtonListener, null);
    }
    if (mForceInverseBackground) {
        dialog.setInverseBackgroundForced(true);
    }
    // For a list, the client can either supply an array of items or an
    // adapter or a cursor
    if ((mItems != null) || (mCursor != null) || (mAdapter != null)) {
        createListView(dialog);
    }
    if (mView != null) {
        if (mViewSpacingSpecified) {
            dialog.setView(mView, mViewSpacingLeft, mViewSpacingTop, mViewSpacingRight,
                    mViewSpacingBottom);
        } else {
            dialog.setView(mView);
        }
    }
}
        
```

实际上就是把P中的参数挨个的设置到AlertController中， 也就是AlertDialog中的mAlert对象。从AlertDialog的各个setter方法中我们也可以看到，实际上也都是调用了mAlert对应的setter方法。在这里，Builder同时扮演了上文中提到的builder、ConcreteBuilder、Director的角色，简化了Builder模式的设计。


### builder模式的优点

#### 易于解耦 
将产品本身与产品创建过程进行解耦，可以使用相同的创建过程来得到不同的产品。也就说细节依赖抽象。
#### 易于精确控制对象的创建 
将复杂产品的创建步骤分解在不同的方法中，使得创建过程更加清晰
#### 易于拓展 
增加新的具体建造者无需修改原有类库的代码，易于拓展，符合“开闭原则“。 

### builder模式的缺点
1. 建造者模式所创建的产品具有较多的共同点，其组成部分相似，如果产品之间的差异性很大，不适合使用建造者模式，因此其使用范围受到一定的限制

2. 如果产品的内部变化复杂，可能会导致需要定义很多具体建造者类来实现这种变化，导致系统变得很庞大，增加系统的理解难度和运行成本。