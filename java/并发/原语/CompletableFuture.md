http://www.itsoku.com/article/190

```java
public static void main(String args[]){

    List<CompletableFuture<List<Integer>>> futures = new ArrayList<>();
    int[] elementProcessors = new int[]{1,2};
    for ( int i = 0;i<elementProcessors.length;i++) {
        int finalI = i;
        CompletableFuture<List<Integer>> future = CompletableFuture.supplyAsync(
                new Supplier<List<Integer>>(){
                    @Override
                    public List<Integer> get() {
                        try {
                            Thread.sleep((finalI +1) * 1000);
                            System.out.println(finalI);
                        } catch (InterruptedException e) {
                            e.printStackTrace();
                        }
                        return new ArrayList<>();
                    }
                    },EXECUTOR_SERVICE);


        futures.add(future);
    }
    for (CompletableFuture<List<Integer>> future : futures) {
        future.join();
    }
    EXECUTOR_SERVICE.shutdown();
    System.out.println("2222222222");
}
```