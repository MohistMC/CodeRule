### Package name rules

* com.mohistmc.[Project Name].
  ```
  com.mohistmc.mohist.*
  com.mohistmc.banner.*  
  ```

### Import rules

* Import the complete class path and prohibit use
  ```
  import com.mohistmc.mohist.* ×
  import com.mohistmc.mohist.Main √
  ```

### Patch project

* Reduce the use of Java lambda, which will break the recognition of Mixins  
  For example: `@Redirect(method = { "lambda$reloadResources$29" }`,   
  if you add a lambda, it will cause the quantity to change, so that `$29` is not correctly identified
  ```
    Wrong usage
    List<String> names = Arrays.asList("Alice", "Bob", "Charlie");
    Collections.sort(names, (a, b) -> a.length() - b.length());
  ```

  ``` 
    Correct usage
    List<String> names = Arrays.asList("Alice", "Bob", "Charlie");
    Collections.sort(names, new Comparator<String>() {
        @Override
        public int compare(String a, String b) {
            return a.length() - b.length();
        }
    });
  ```