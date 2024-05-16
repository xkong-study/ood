1.静态成员变量      
使用public static修饰的成员变量是静态成员变量，它们属于类本身，而不是属于类的实例。     
静态成员变量在类加载时就会被分配内存空间，并且所有类的实例都共享同一个静态成员变量。通常情况下，静态成员变量用于表示类级别的属性或常量。       
```code
public class Example {
    public static int count = 0; // 静态成员变量
}

```

2.静态方法     
使用public static修饰的方法是静态方法，它们也属于类本身，而不是属于类的实例。静态方法可以直接通过类名调用，而不需要创建类的实例。     
通常情况下，静态方法用于执行与类相关的操作，而不需要访问实例的特定状态。      
方法不依赖于特定的对象状态。       

```code
public class Example {
    public static void printMessage() {
        System.out.println("Hello, world!");
    }
}

```

在面向对象的编程中，将相关的方法和属性组织在一个类中是一种常见的做法，即使这些方法和属性不需要依赖特定的对象实例也是如此。这样做的好处包括：     

逻辑上的组织：将相关的方法和属性放在同一个类中可以更好地组织代码，使代码更具可读性和可维护性。   

易于管理：将所有相关的方法和属性放在同一个地方，有助于开发人员更容易找到并理解与特定类相关的所有功能。      

```code
public class BookReservation {
private Date creationDate;
private ReservationStatus status;
private String bookItemBarcode;
private String memberId;
public static BookReservation fetchReservationDetails (String barcode);
}
public class BookLending {
private Date creationDate;
private Date dueDate;
private Date returnDate;
private String bookItemBarcode;
private String memberId;
public static void lendBook (String barcode, String memberId);
public static Bookending fetchLendingDetails (String barcode);
}
```

怎么判断这个方法要不要实例化才要调用呢？     要修改对象的状态或属性的时候         

实例相关操作：如果方法需要访问或修改特定对象实例的状态或属性，则通常需要实例化对象才能调用该方法。例如，如果一个方法需要访问对象的属性或调用对象的其他方法，那么这个方法可能需要实例化才能调用。          

静态操作：如果方法不需要访问特定对象的状态或属性，并且其功能独立于对象实例，则通常可以将该方法声明为静态方法。静态方法可以直接通过类名调用，而不需要先创建类的实例。      

工具类方法：有些方法可能提供一些通用的功能，与特定对象实例无关，这样的方法通常被声明为静态方法，并且可以在不创建对象实例的情况下调用。      

fetchReservationDetails 方法：    

这个方法可能用于从数据库或其他存储系统中检索特定书籍的预订详情。     
由于它是针对特定的书籍条形码（barcode）进行操作，而不是与特定的 BookReservation 实例相关联的操作，因此它被声明为静态方法。    
这样一来，你可以通过 BookReservation.fetchReservationDetails(barcode) 的方式直接调用该方法，而不需要先创建 BookReservation 实例。    

lendBook 方法：    

这个方法可能用于将书籍借出给特定的会员（member）。    
同样地，它与特定的 BookLending 实例无关，因为它只是执行一项操作而不涉及任何特定的对象状态。   
因此，它也被声明为静态方法，以便可以通过 BookLending.lendBook(barcode, memberId) 的方式直接调用。    

uml写法：   
```code
<<static>> methodName(parameters) : returnType
```
