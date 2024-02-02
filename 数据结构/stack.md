```code
import java.util.Stack;

public class StackExample {
    public static void main(String[] args) {
        // 创建一个 Stack 对象
        Stack<Integer> stack = new Stack<>();

        // 入栈
        stack.push(1);
        stack.push(2);
        stack.push(3);

        // 出栈
        int poppedElement = stack.pop();
        System.out.println("Popped element: " + poppedElement);

        // 查看栈顶元素
        int topElement = stack.peek();
        System.out.println("Top element: " + topElement);

        // 判断栈是否为空
        boolean isEmpty = stack.isEmpty();
        System.out.println("Is the stack empty? " + isEmpty);
    }
}

```
