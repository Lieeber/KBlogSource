---
title: 用Java实现各种排序
tags:
  - 排序
  - 数据结构
categories:
  - 数据结构
date: 2017-06-18 21:22:15
---
用Java实现各种排序。
<!-- more -->
```java
public class Sort {
    private void swap(int[] arrs, int i, int j) {
        int temp = arrs[i];
        arrs[i] = arrs[j];
        arrs[j] = temp;
    }
    /**
     * 冒泡排序基本版
     */
    private void bubbleSort(int[] arrs) {
        for (int i = 0; i < arrs.length; i++) {
            for (int j = arrs.length - 2; j >= i; j--) {
                System.out.println("--------------------");
                if (arrs[j] > arrs[j + 1]) {
                    swap(arrs, j, j + 1);
                }
            }
        }
    }

    /**
     * 冒泡排序改进版
     * 改进版的效率要高很多，遍历的次数明显减少了。
     */
    private void bubbleSort2(int[] arrs) {
        boolean flag = true;
        for (int i = 0; i < arrs.length && flag; i++) {
            flag = false;
            for (int j = arrs.length - 2; j >= i; j--) {
                System.out.println("--------------------");
                if (arrs[j] > arrs[j + 1]) {
                    swap(arrs, j, j + 1);
                    flag = true;
                }
            }
        }
    }

    @Test
    public void testBubbleSort() {
        int[] arrs = {12, 3, 44, 55, 11, 13, 9, 66, 78, 0, 54, 88};
        bubbleSort(arrs);
        System.out.println(Arrays.toString(arrs));

        bubbleSort2(arrs);
        System.out.println(Arrays.toString(arrs));
    }


    /**
     * 简单选择排序算法
     */
    private void selectSort(int[] arrs) {
        for (int i = 0; i < arrs.length; i++) {
            int min = i;//默认定义第一个元素的下标是最小元素的下标
            for (int j = i + 1; j < arrs.length; j++) {
                System.out.println("++++++++++++++++++");
                if (arrs[min] > arrs[j]) {  //让第一个元素与剩下的所有元素比较，取出最小元素的下标赋值给min
                    min = j;
                }
            }
            if (i != min) {//如果最小元素的下标不是第一个了，证明中间有比第一个元素要小的元素，让第一个元素与该元素进行交换
                swap(arrs, i, min);
                System.out.println("--------------------");
            }
        }
    }

    @Test
    public void testSelectSort() {
        int[] arrs = {12, 3, 44, 55, 11, 13, 9, 66, 78, 0, 54, 88};
        selectSort(arrs);
        System.out.println(Arrays.toString(arrs));

    }


    /**
     * 直接插入排序算法
     */
    private void insertSort(int[] arrs) {
        for (int i = 1; i < arrs.length; i++) {
            int temp = arrs[i]; //取出一个待插入的记录
            int j;
            for (j = i - 1; j >= 0; j--) {
                System.out.println("--------------------");
                if (temp < arrs[j]) {   //从后往前遍历已经排好序的有序表，判断带插入记录与其中每个记录的大小，如果待插入记录要小于有序表中的某个记录，就将有序表中该记录往后移动，空出一个位置，如果不小于，则终止循环。
                    arrs[j + 1] = arrs[j];
                } else {
                    break;
                }
            }
            arrs[j + 1] = temp;    //将空出的这个位置赋值为待插入的元素。
        }
    }

    @Test
    public void testInsertSort() {
        int[] arrs = {12, 3, 44, 55, 11, 13, 9, 66, 78, 0, 54, 88};
        insertSort(arrs);
        System.out.println(Arrays.toString(arrs));
    }


    /**
     * 希尔排序
     * 和直接插入排序的算法形式是一样的，只不过加入了一个步长。
     */
    private void shellSort(int[] arrs) {
        int temp;
        int j;
        for (int increment = arrs.length / 2; increment > 0; increment /= 2) {
            for (int i = increment; i < arrs.length; i++) {
                temp = arrs[i];
                for (j = i - increment; j >= 0; j -= increment) {
                    System.out.println("--------------------");
                    if (temp < arrs[j]) {
                        arrs[j + increment] = arrs[j];
                    } else {
                        break;
                    }
                }
                arrs[j + increment] = temp;
            }
        }
    }

    @Test
    public void testShellSort() {
        int[] arrs = {12, 3, 44, 55, 11, 13, 9, 66, 78, 0, 54, 88};
        shellSort(arrs);
        System.out.println(Arrays.toString(arrs));
    }


    /**
     * 堆排序
     */
    private void heapSort(int[] arrs) {
        int i;
        for (i = arrs.length / 2 - 1; i >= 0; i--) {// 构建一个大顶堆
            adjustHeap(arrs, i, arrs.length - 1);
        }
        for (i = arrs.length - 1; i >= 0; i--) {// 将堆顶记录和当前未经排序子序列的最后一个记录交换
            int temp = arrs[0];
            arrs[0] = arrs[i];
            arrs[i] = temp;
            adjustHeap(arrs, 0, i - 1);// 将a中前i-1个记录重新调整为大顶堆
        }
    }

    private void adjustHeap(int[] arrs, int i, int len) {
        int temp, j;
        temp = arrs[i];
        for (j = 2 * i; j < len; j *= 2) {// 沿关键字较大的孩子结点向下筛选
            if (j < len && arrs[j] < arrs[j + 1])
                ++j; // j为关键字中较大记录的下标
            if (temp >= arrs[j])
                break;
            arrs[i] = arrs[j];
            i = j;
        }
        arrs[i] = temp;
    }

    @Test
    public void testHeapSort() {
        int[] arrs = {12, 3, 44, 55, 11, 13, 9, 66, 78, 0, 54, 88};
        heapSort(arrs);
        System.out.println(Arrays.toString(arrs));
    }


    /**
     * 归并排序
     */
    private void mergeSort(int[] arrs) {
        mSort(arrs, 0, arrs.length - 1);
    }

    private void mSort(int[] arrs, int low, int high) {
//      int mid = (low + high) / 2;
        int mid = low + (high - low) / 2;
        if (low < high) {
            //左边
            mSort(arrs, low, mid);
            //右边
            mSort(arrs, mid + 1, high);
            //左右合并
            merge(arrs, low, mid, high);
        }
    }

    private  void merge(int[] arrs, int low, int mid, int high) {
        int[] temp = new int[high - low + 1];
        int i = low;// 左指针
        int j = mid + 1;// 右指针
        int k = 0;
        // 把较小的数先移到新数组中
        while (i <= mid && j <= high) {
            if (arrs[i] < arrs[j]) {
                temp[k++] = arrs[i++];
            } else {
                temp[k++] = arrs[j++];
            }
        }
        // 把左边剩余的数移入数组
        while (i <= mid) {
            temp[k++] = arrs[i++];
        }
        // 把右边边剩余的数移入数组
        while (j <= high) {
            temp[k++] = arrs[j++];
        }
        // 把新数组中的数覆盖nums数组
        for (int k2 = 0; k2 < temp.length; k2++) {
            arrs[k2 + low] = temp[k2];
        }
    }

    @Test
    public void testMergeSort() {
        int[] arrs = {12, 3, 44, 55, 11, 13, 9, 66, 78, 0, 54, 88};
        mergeSort(arrs);
        System.out.println(Arrays.toString(arrs));
    }


    /**
     * 快速排序
     */
    private void quickSort(int[] arrs) {
        qSort(arrs, 0, arrs.length - 1);
    }

    private void qSort(int[] arrs, int low, int high) {
        int mid;
        if (low < high) {
            mid = partition(arrs, low, high);
            qSort(arrs, low, mid);
            qSort(arrs, mid + 1, high);
        }
    }

    private int partition(int[] arrs, int low, int high) {
        int midKey = arrs[low]; //用子表的第一个记录作为枢轴记录
        while (low < high) {    //从表的两端交替向中间扫描
            while (low < high && arrs[high] >= midKey) {
                high--;
            }
            swap(arrs, low, high);  //将比枢轴记录小的记录交换到左边
            while (low < high && arrs[low] <= midKey) {
                low++;
            }
            swap(arrs, low, high);  //将比枢轴记录大的记录交换到右边
        }
        return low;
    }

    @Test
    public void testQuickSort() {
        int[] arrs = {1000,2,3,418,5,100,7,8,9,10,101,242,33,44,55};
        quickSort(arrs);
        System.out.println(Arrays.toString(arrs));
    }
}
```