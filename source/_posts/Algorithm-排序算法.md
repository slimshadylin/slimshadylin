---
title: Algorithm-排序算法
top: false
cover: false
toc: true
mathjax: true
date: 2020-12-20 14:45:35
password:
summary:
tags:
- Algorithm
categories:
- 算法
---

# 归并排序

1. 算法思想

2. 算法过程

3. 流程图

4. java实现

    ``` java
    public class MergeSort {

        public static void process(int[] arr, int left, int right) {
            if (arr == null || arr.length <= 1) {
                return;
            }
            mergeSort(arr, left, right);
        }

        public static void mergeSort(int[] arr, int left, int right) {
            if (left == right) {
                return;
            }
            int mid = left + ((right - left) >> 1);
            mergeSort(arr, left, mid);
            mergeSort(arr, mid + 1, right);
            merge(arr, left, mid, right);
        }

        public static void merge(int[] arr, int left, int mid, int right) {
            int[] helpArray = new int[right - left + 1];
            int h = 0;
            int l = left;
            int r = mid + 1;
            while (l <= mid && r <= right) {
                helpArray[h++] = arr[l] < arr[r] ? arr[l++] : arr[r++];
            }
            while (l <= mid) {
                helpArray[h++] = arr[l++];
            }
            while (r <= right) {
                helpArray[h++] = arr[r++];
            }
            for (int i = 0; i < helpArray.length; i++) {
                arr[left + i] = helpArray[i];
            }
        }

        public static void main(String[] args) {
            int[] arr = {1, 43, 55, 88, 33, 12, 34, 56, 9};
            process(arr, 0, arr.length - 1);
            for (int i : arr) {
                System.out.println(i);
            }
        }
    }

    ```

# 快速排序

1. 排序思想
    * 随机取数组中的一个值，作为基准key；（通过概率让时间复杂度从$O(N^2)$降低到$O(N*\log{N})$）
    * 进行荷兰国旗划分，小于key的值在左边，等于key的所有值在中间（可能有多个），大于key的值在右边
    * 分别对左右两边的子区域递归进行荷兰国旗划分
    * 最终子问题不能再划分的时候，快速排序就完成了

2. 算法过程

3. 流程图

4. java代码实现

    ``` java
    public class QuickSort {
        public static void process(int[] arr) {
            if (arr == null || arr.length < 2) {
                return;
            }
            quickSort(arr, 0, arr.length - 1);
        }

        public static void quickSort(int[] arr, int left, int right) {
            // 选取一个位置的数和right位置的数交换、每次都以right位置的数作为荷兰国旗划分的flag
            int sortKey = left + (int) (Math.random() * (right - left + 1)); // 0.00 <= Math.random() < 1.00
            swap(arr, sortKey, right);
            int[] equalArea = partition(arr, left, right);
            quickSort(arr, left,equalArea[0] - 1);
            quickSort(arr, equalArea[1] + 1, right);

        }

        /**
        @param arr 待排序数组
        @param left 左边界的下标
        @param right 右边界的下标
        @return 返回flag的左右边界的位置（包含两个元素的数组，第一个是左边界，第二个是右边界）
        */
        public static int[] partition(int[] arr, int left, int right) {
            if (left > right) {
                return new int[] {-1, -1};
            }
            if (left == right) {
                return new int[] {left, right};
            }
            int less = left - 1; // 小于区域的右边界
            int more = right; // 大于区域的左边界
            int index = left;
            while (index < more) {
                if (arr[index] < arr[right]) {
                    swap(arr, ++less, index++);

                } else if (arr[index] == arr[right]) {
                    index++;

                } else {
                    swap(arr, --more, index);
                }
            }
            swap(arr, more, right); // 把基准值和大于区域左边界的值交换，这样才能保证，基准值左边的数都比它小，右边的数都比它大
            return new int[] {less + 1, more};
        }

        public static void swap(int[] arr, int i, int j) {
            // 如果i和j位置相同，异或后恒为0
            if (i == j) {
                return;
            }
            arr[i] = arr[i] ^ arr[j];
            arr[j] = arr[i] ^ arr[j];
            arr[i] = arr[i] ^ arr[j];
        }

        public static void main(String[] args) {
            int[] arr = {1, 3, 3, 5, 5, 7, 1, 2};
            process(arr);
        }
    }
    ```

# 堆排序

## 堆的概念

1. 堆是一个数组

2. 堆是一棵完全二叉树（在一颗二叉树中，若除最后一层外的其余层都是满的，并且最后一层要么是满的，要么在右边缺少连续若干节点，则此二叉树为完全二叉树（Complete Binary Tree））
3. 堆分为大根堆和小根堆，大根堆的root节点值最大，小根堆的root节点值最小

4. 如果堆的根节点从数组的第1个位置开始，那么有以下结论：

    * 左子树的父节点可以用`i >> 1`表示；

    * 右子树的父节点可以用`i >> 1 | 1`；

    * 父节点找左子树`i << 1`;

    * 父节点找右子树`i << 1 | 1`;

下图所示的就不是堆，因为最后一层缺少的节点并不是全在右边，而是间隔出现的
![不是堆](不是堆.png)

## 堆排序的流程图

1. 以下方法以大根堆为例

    ① 首先把原数组调整为一个大根堆
    ② 接着把根节点和数组的最后一个节点交换，数组的右边界减一；
    ③ 重复步骤1和步骤2
    ④ 除了第一调整大根堆的时间复杂度是$O\left(N\right)$，剩余的每一次调整大根堆都是$O\left(\log{N}\right)$,总体需要N次，所以总的时间复杂度是$O\left(N*\log{N}\right)$

2. 第一次调整为大根堆流程如下：

    从根节点，依次遍历所有的几点，每个节点都需要进行上浮操作，直到满足之前节点的父节点都比子节点大
    ① 初始数组[-59, -33, 37, -81, 69, 18, 26, -1, -26, 29, -67, -50, -20, -38, 32]
    ![初始数组](1.png)
    ② 0位置没有父节点，不做任何操作
    ![0位置调整](2.png)
    ③ 1位置的数比父节点大，需要交换
    ![1位置调整](3.png)
    ④ 2位置的数比父节点大，需要交换
    ![2位置调整](4.png)
    ⑤ 3位置的数比父节点小，不做任何操作
    ![3位置调整](5.png)
    ⑥ 4比父节点大，需要交换，交换后还比父父节点大，再交换
    ![4位置调整](6.png)
    ⑦ 5比父节点大，需要交换，然后再比父父节点小，不交换
    ![5位置调整](7.png)
    ⑧ 6比父节点大，需要交换，然后再比父父节点小，不交换
    ![6位置调整](8.png)
    ⑨ 7比父节点大，需要交换，然后再比父父节点小，不交换
    ![7位置调整](9.png)
    ⑩ 8比父节点小，不做任何操作
    ![8位置调整](10.png)
    ⑪ 9比父节点大，需要交换，然后再比父父节点小，不交换
    ![9位置调整](11.png)
    ⑫ 10比父节点小，不做任何操作
    ![10位置调整](12.png)
    ⑬ 11比父节点小，不做任何操作
    ![11位置调整](13.png)
    ⑭ 12比父节点大，需要交换，然后再比父父节点小，不交换
    ![12位置调整](14.png)
    ⑮ 13比父节点小，不做任何操作
    ![13位置调整](15.png)
    ⑯ 14比父节点大，需要交换，然后再比父父节点大，需要交换，然后再比父父父节点小，不交换
    ![14位置调整](16.png)

3. 交换根节点和最后一位节点的数，开始找第二大的节点

    ![最大的节点](sort1.png)
    ![第二大的节点](sort2.png)

4. 交换根节点和倒数第二个节点的数，开始找第三大的节点

    ![交换节点](sort3.png)
    ![第三大的节点](sort4.png)

5. 依次重复，直到所有元素排好序，可以看出每次根节点交换后再形成大根堆的时间复杂度是$O\left(\log{N}\right)$，需要进行N次，所以总的时间复杂度是$O\left(N*\log{N}\right)$

## java实现

``` java
public class HeapSort {
    public static void heapSort(int[] arr) {
        int size = arr.length;
        if (arr == null || size < 2) {
            return;
        }
        // 构建初始大根堆
        for (int i = 0; i < size; i++) {
            heapInsert(arr, i);
        }
        // 交换最后一位和根节点的位置，并移除堆尾元素
        swap(arr, 0, --size);
        while(size > 0) {
            heapify(arr, 0, size);
            swap(arr, 0, --size);
        }
    }

    /** index位置的数和父节点比大小 */
    private static void heapInsert(int[] arr, int index) {
        while (arr[index] > arr[(index - 1) / 2]) {
            swap(arr, index, (index - 1) / 2);
            index = (index - 1) / 2;
        }
    }

    private static void swap(int[] arr, int i, int j) {
        int temp = arr[i];
        arr[i] = arr[j];
        arr[j] = temp;
    }

    /** index位置的数和子节点比大小 */
    private static void heapify(int[] arr, int start, int end) {
        int left = start * 2 + 1;
        while (left < end) {
            // 两个孩子中，谁的值大，把下标给largest
            // 1）只有左孩子，left -> largest
            // 2) 同时有左孩子和右孩子，右孩子的值<= 左孩子的值，left -> largest
            // 3) 同时有左孩子和右孩子并且右孩子的值> 左孩子的值， right -> largest
            int max = left + 1 < end && arr[left] < arr[left + 1] ? left + 1 : left;
            // 当孩子中的最大值比父节点大，交换
            max = arr[start] < arr[max] ? max : start;
            if (start == max) {
                break;
            }
            swap(arr, start, max);
            start = max;
            left = start * 2 + 1;
        }
    }

    public static void main(String[] args) {
        int[] arr = {16, 7, 3, 20, 17, 8};
        heapSort(arr);
        for (int i : arr) {
            System.out.println(i);
        }
    }

}
```

# 桶排序

## 原理分析

对于基于比较的排序，最好的时间复杂度是$O\left(N*\log{N}\right)$，而桶排序的时间复杂度可以达到$O\left(N\right)$，它假设输入数据服从均匀分布，我们将数据分别放入到 n 个桶内，先对桶内数据进行排序，然后遍历桶依次取出桶中的元素即可完成排序。

和计数排序类似，桶排序也对输入数据作了某种假设，因此它的速度也很快。具体来说，计数排序假设了输入数据都属于一个小区间内的整数，而桶排序则假设输入数据是均匀分布的，即落入每个桶中的元素数量理论也是差不多的，不会出现很多数落入同一个桶内的情况。

无论是桶排序还是计数排序，都需要事先对数据的状况有比较好的掌握，一旦数据的分布有所变化，可能代码就需要大面积修改。

## 示例分析

* 要求：对N个非负的数字进行排序。

* 思想：申请10个桶，每个桶分别代表当前位数为0~9的数，依次从个位放入倒出，完成个位从小到大的排列，十位、百位重复操作，最后就能完成所有数的排序，每次的时间复杂度是$O\left(N\right)$，需要M（M的值和最大值的位数有关，是一个和数据量无关的常量）次，总的时间复杂度还是$O\left(N\right)$。

* java代码实现

    ``` java
    public class BucketSort {

        public static void bucketSort(int[] arr) {
            if (arr == null || arr.length < 2) {
                return;
            }
            radixSort(arr, 0, arr.length - 1, getMaxBits(arr));
        }

        /** 获取数组中最大值由多少个数字组成，比如 87654是最大值，那么返回5 */
        private static int getMaxBits(int[] arr) {
            int maxNum = Integer.MIN_VALUE;
            for(int i = 0; i < arr.length - 1; i++) {
                maxNum = Math.max(maxNum, arr[i]);
            }
            int res = 0;
            while (maxNum != 0) {
                res++;
                maxNum /= 10;
            }
            return res;
        }

        /** 对数组L~R位置上进行基数排序
        * @param arr 数组
        * @param L 起始位置
        * @param R 结束位置
        * @param digit 最大值的数字个数
        */
        private static void radixSort(int[] arr, int L, int R, int digit) {
            // 0~9的10个数字
            final int radix = 10;
            int i = 0, j = 0;
            int[] help = new int[R - L + 1];
            // digit有多少位，每个数字都要遍历多少遍
            for (int d = 1; d <= digit; d++) {
                // 存放数字0~9
                int[] count = new int[radix];
                // 下面的方法实现了如下功能
                // count[0] 表示第d位的数字，值等于0的个数
                // count[1] 表示第d位的数字，值在区间0~1的个数
                // count[2] 表示第d位的数字，值在区间0~2的个数
                // count[3] 表示第d位的数字，值在区间0~3的个数
                // ...
                // count[n] 表示第d位的数字，值在区间0~n的个数
                for (i = L; i <= R; i++) {
                    j = getDigit(arr[i], d);
                    count[j]++;
                }
                for (i = 1; i < radix; i++) {
                    count[i] = count[i] + count[i - 1];
                }
                for (i = R; i >= L; i--) {
                    j = getDigit(arr[i], d);
                    help[count[j] - 1] = arr[i];
                    count[j]--;
                }
                for (i = L, j = 0; i <= R; i++, j++) {
                    arr[i] = help[j];
                }
            }

        }


        /** 获取指定位数上的数值，比如12345，第一位是5，第二位是4...第5位是1
        * @param num 数字，如12345
        * @param d 第n位
        * @return 第n位的值
        */
        private static int getDigit(int num, int d) {
            return ((num / ((int) Math.pow(10, d - 1))) % 10);
        }

        public static void main(String[] args) {
            int[] arr = {68531, 62888, 70154, 49349, 66527, 84477, 59921, 27085, 36227, 12834};
            bucketSort(arr);
            for (int i : arr) {
                System.out.println(i);
            }
        }

    }
    ```

* 需要注意的点：算法中只用了两个固定长度的数组，模拟了10个桶的入桶出桶操作，非常巧妙，但是比较难理解；对于判断数字中每个位数的值需要考虑部分数字位数小于最大值，需要最高位补零

# 排序总结

## 复杂度和稳定性总结

| 排序算法 | 时间复杂度 | 空间复杂度 | 稳定性 |
| -------- | ---------- | ---------- | ------ |
| 选择排序 | $O(N^2)$    | $O(1)$  |   无    |
| 冒泡排序 | $O(N^2)$    | $O(1)$  |   有   |
| 插入排序 | $O(N^2)$    | $O(1)$  |   有   |
| 归并排序 | $O(N*\log{N})$ | $O(N)$ |  有    |
| 随机快排 | $O(N*\log{N})$ | $O(\log{N})$ |   无   |
| 堆排序   | $O(N*\log{N})$ | $O(1)$ |  无  |
| 计数排序 | $O(N)$      |  $O(M)$  |   有   |
| 基数排序 | $O(N)$      |  $O(N)$  |   有   |


## 结论

1. 除了计数排序和基数排序，都是基于比较的排序

2. 不基于比较的排序，对样本数据有严格的要求，不易改写（样本变化，改写的代价很大）

3. 基于比较的排序，只需要规定样本怎么比较大小，就可以复用（各种语言的排序算法都是基于比较的排序）

4. 基于排序的算法，理论的极限时间复杂度是$O(N*\log{N})$

5. 时间复杂度为$O(N*\log{N})$，空间复杂度小于$O(N)$，且稳定的基于比较的排序是不存在的

6. 为了绝对的速度选择快排（常数项最小，优于归并和堆排序），省空间选堆排序，为了稳定性选择归并排序

## 常见的坑

1. 归并排序的额外空间复杂度可以优化成$O(1)$，“归并排序 内部缓存法”，但是会变得不再稳定（直接用堆排序就行，这个很难懂，且没有太大的实际意义）

2. “01 stable sort”算法

# 工业级排序实现

1. 如果是基础数据类型，用快排，如果是非基础数据类型，用归并排序（不破坏稳定性）

2. 对于小于60个数的样本量，直接用插入排序，虽然时间复杂度高，但是常数项小，总体来说，小样本量的时间其实会优于快排
