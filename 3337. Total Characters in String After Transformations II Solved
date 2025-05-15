import java.util.List;

class Solution {
    private static final long MOD = 1000000007;

    public int lengthAfterTransformations(String s, int t, List<Integer> nums) {
        int n = s.length();
        long[] initialCounts = new long[26];
        for (char c : s.toCharArray()) {
            initialCounts[c - 'a']++;
        }

        long[][] transformationMatrix = new long[26][26];
        for (int i = 0; i < 26; i++) {
            int expandsTo = nums.get(i);
            for (int j = 1; j <= expandsTo; j++) {
                transformationMatrix[i][(i + j) % 26] = (transformationMatrix[i][(i + j) % 26] + 1) % MOD;
            }
        }

        long[][] finalTransformation = power(transformationMatrix, t);

        long finalLength = 0;
        for (int i = 0; i < 26; i++) {
            for (int j = 0; j < 26; j++) {
                finalLength = (finalLength + (initialCounts[i] * finalTransformation[i][j]) % MOD) % MOD;
            }
        }

        return (int) finalLength;
    }

    private long[][] multiply(long[][] a, long[][] b) {
        int size = a.length;
        long[][] result = new long[size][size];
        for (int i = 0; i < size; i++) {
            for (int j = 0; j < size; j++) {
                for (int k = 0; k < size; k++) {
                    result[i][j] = (result[i][j] + (a[i][k] * b[k][j]) % MOD) % MOD;
                }
            }
        }
        return result;
    }

    private long[][] power(long[][] base, int exp) {
        int size = base.length;
        long[][] result = new long[size][size];
        for (int i = 0; i < size; i++) {
            result[i][i] = 1;
        }
        while (exp > 0) {
            if ((exp & 1) == 1) {
                result = multiply(result, base);
            }
            base = multiply(base, base);
            exp >>= 1;
        }
        return result;
    }
}
