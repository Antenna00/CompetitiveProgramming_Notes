Sieve of Eratosthenes (エラトステネスのふるい)
Premise: 

		Input: Integer value, boolean (optional for sorting the array)
		Usage: To create the array list that consists the prime number below the input value
![[Sieve_of_Eratosthenes_animation.gif]]

Overall Process: 

	Prepare boolean array to manage this algorithm. 
	Boolean array will be used to eliminate the non-prime number.
	 

	1. Fill the boolean array with "True"
	2. for (int i = 2; i * i <= n; ++i) for multiple of 2, multiple of 3, multiple of 5 and so on...
	3. if boolean array of i is found "True", subsitute "False" instead to mark as non-prime number.
	4. Repeat the process 2 ~ 3
	5. Result in list of prime number in array.
	
```Java
 public static <T> Vector<?> eratosthenesPrimeList(T N, boolean greater) {
 
        long n = (long) N;
        Vector<Long> vec = new Vector<>();
        Vector<Boolean> vprime = new Vector<>();
        vprime.setSize((int) n + 1);
        
        // 全てにTrueを設定。Javaでは初期化時に設定できない模様。糞仕様である。
        // for (int o = 0; o < vprime.size(); ++o) {
        // //.addだと最後の値がシフトされる
        // vprime.add(o, true);
        // }
        // Collections.replaceAll(vprime, false, true);
		
        Collections.fill(vprime, true);
        
        for (int i = 2; i * i <= n; ++i) {
            // xの倍数のindexをfalseに置換
            if (vprime.get(i) == true) {
                for (int x = 2 * i; x <= n; x += i)
                    vprime.set(x, false);
            }
        }
        if (greater) {
            for (long j = 2; j <= n; ++j) {
                // forloop内でキャストしたくない・・・。
                // 後の改善ポイント？ただ素数がint範囲以上の場合もあるのでとりあえず妥協。
                if (vprime.get((int) j))
                    vec.add(j);
            }
            Collections.sort(vec); // 昇順設定 ここも早くするなら自分でUtility書いたほうがいい。改善ポイント。
        } else {
            for (long k = 2; k <= n; ++k) { // これ記述量減らせるんでは。
                if (vprime.get((int) k))
                    vec.add(k);
            }
            Collections.sort(vec);
            Collections.reverse(vec); // 降順に変更
        }
        
        return vec;
    }
```