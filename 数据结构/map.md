1.V computeIfAbsent(K key, Function<? super K, ? extends V> mappingFunction)
2.V getOrDefault(Object key, V defaultValue)


基本操作：    

V put(K key, V value): 将指定的值与该映射中的指定键关联，如果已存在该键，则替换旧值。      
V get(Object key): 返回指定键映射到的值，如果不存在，则返回 null。       
boolean containsKey(Object key): 如果此映射包含指定键的映射关系，则返回 true。     
boolean containsValue(Object value): 如果此映射将一个或多个键映射到指定值，则返回 true。         
int size(): 返回此映射中的键-值映射关系数。    

修改操作：

V remove(Object key): 从该映射中移除指定键的映射关系（如果存在）。      
void putAll(Map<? extends K, ? extends V> m): 将指定映射的所有映射关系复制到此映射中。     
void clear(): 从该映射中移除所有映射关系。 

获取视图：      

Set<K> keySet(): 返回此映射中包含的键的 Set 视图。   
Collection<V> values(): 返回此映射中包含的值的 Collection 视图。    
Set<Map.Entry<K, V>> entrySet(): 返回此映射中包含的映射关系的 Set 视图。         

默认值：          

V getOrDefault(Object key, V defaultValue): 返回指定键映射到的值，如果键不存在，则返回指定的默认值。         

合并和计算：                         

V merge(K key, V value, BiFunction<? super V, ? super V, ? extends V> remappingFunction): 如果指定的键不存在（或映射到 null 值），则将其与给定的非 null 值关联；否则，使用给定的 remapping 函数计算新值，并将其替换旧值。                                                        

V compute(K key, BiFunction<? super K, ? super V, ? extends V> remappingFunction): 如果指定键的映射存在且非 null，则尝试根据给定的 remapping 函数计算新映射值。

V computeIfAbsent(K key, Function<? super K, ? extends V> mappingFunction): 如果指定的键尚未与值关联（或映射到 null），则尝试使用给定的映射函数计算其值。

V computeIfPresent(K key, BiFunction<? super K, ? super V, ? extends V> remappingFunction): 如果指定的键在映射中存在且其值不为 null，则尝试使用给定的 remapping 

函数重新计算其值。                         

