```code
public interface Set<E> extends Collection<E> {
    boolean add(E e);
    boolean remove(Object o);
    void clear();
    boolean contains(Object o);
    int size();
    boolean isEmpty();
    Iterator<E> iterator();
    Object[] toArray();
    <T> T[] toArray(T[] a);
    String toString();
}
```
