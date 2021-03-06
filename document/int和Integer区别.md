## int和Integer基本区别
> 1. Integer是int的包装类， int则是java的一种基本数据类型
> 2. Integer变量必须实例化后才能使用，而int变量不需要
> 3. Integer实际是对象的引用，当new一个Integer时，实际上是生成一个指针指向此对象，而int则是直接存储数据值
> 4. Integer的默认值是null，int的默认值是0

## Integer和int判等 
> 1. int 和Integer在进行比较的时候，Integer会进行拆箱，转为int值与int进行比较。
> 2. Integer与Integer比较的时候，由于直接赋值的时候会进行自动的装箱，那么这里就需要注意两个问题，
>>  * 个是-128<= x<=127的整数，将会直接缓存在IntegerCache中，那么当赋值在这个区间的时候，不会创建新的Integer对象，而是从缓存中获取已经创建好的Integer对象。

>> * 当大于这个范围的时候，直接new Integer来创建Integer对象。

>> * new Integer(1) 和Integer a = 1不同，前者会创建对象，存储在堆中，而后者因为在-128到127的范围内，不会创建新的对象，而是从IntegerCache中获取的。那么Integer a = 128, 大于该范围的话才会直接通过new Integer（128）创建对象，进行装箱。


	int i = 128;
        Integer i2 = 128;
        Integer i3 = new Integer(128);
        //Integer会自动拆箱为int，所以为true
        System.out.println(i == i2);
        System.out.println(i == i3);
        System.out.println("**************");
        Integer i5 = 127;//java在编译的时候,被翻译成-> Integer i5 = Integer.valueOf(127);
        Integer i6 = 127;
        System.out.println(i5 == i6);//true
        /*Integer i5 = 128;
        Integer i6 = 128;
        System.out.println(i5 == i6);//false*/      
		Integer ii5 = new Integer(127);
        System.out.println(i5 == ii5); //false
        Integer i7 = new Integer(128);
        Integer i8 = new Integer(123);
        Integer i9 = Integer.valueOf(128);
        Integer i10 = new Integer(128);
        System.out.println(i7 == i8);  //false
        System.out.println(i9 == i10);
        /*out
         *true
         *
		 *true
		 *false
		 *false
		 *false
         */

>
> 更加深入的讲解
>> https://www.cnblogs.com/liaoweipeng/p/6263091.html <br>
>> http://www.cnblogs.com/vinozly/p/5173477.html