# Greedy-4

## Problem1: Minimum Path Form String formation

https://leetcode.com/problems/shortest-way-to-form-string/

//Time Complexity = O(N \* logN)
//Space Complexity = O(N)

class Solution {
public int shortestWay(String source, String target) {
if(source == null){
return -1;
}
if(source.length() == 0 && target.length() == 0) {
return 0;
}
if(source.equals(target)) {
return 1;
}
int position = 0;
int i = 0;
int result = 1;
int tlength = target.length();
int slength = source.length();

        HashMap<Character,List<Integer>> map = new HashMap<>();

        for(int j = 0; j < slength; j++) {
            char c = source.charAt(j);
            if(!map.containsKey(c)) {
                map.put(c, new ArrayList<>());
            }
            map.get(c).add(j);
        }

        while(i < tlength) {
            char c = target.charAt(i);
            if(!map.containsKey(c)) {
                return -1;
            }

            List<Integer> idxList = map.get(c);
            int bIdx = binarySearch(idxList, position);

            if(bIdx == idxList.size()) {
                position = 0;
                result++;
            } else {
                position = idxList.get(bIdx) + 1;
                i++;
            }
        }

        return result;
    }

    private int binarySearch(List<Integer> list,int target) {
        int low = 0;
        int high = list.size()-1;

        while(low <= high) {
            int mid = low + (high - low) /2;
            if(target == list.get(mid)) {
                return mid;
            } else if (list.get(mid) > target) {
                high = mid - 1;
            } else {
                low = mid + 1;
            }
        }
        return low;
    }

}

## Problem2: Equal Row From Minimum Domino Rotations

https://leetcode.com/problems/minimum-domino-rotations-for-equal-row/

//Time Complexity = O(N)
//Space Complexity = O(1)

class Solution {
public int minDominoRotations(int[] tops, int[] bottoms) {
if(tops == null || tops.length == 0) {
return -1;
}
int n = tops.length;
int result = rotations(tops,bottoms, tops[0]);

        if(result != -1) {
            return result;
        }
        return rotations(tops,bottoms,bottoms[0]);

    }

    private int rotations(int[] tops, int[] bottoms, int target) {
        int trot = 0;
        int brot = 0;
        int n = tops.length;
        for(int i = 0 ; i < n; i++) {
            if(tops[i] != target && bottoms[i] != target) {
                return -1;
            }
            if(tops[i] != target) {
                trot++;
            }
            if(bottoms[i] != target) {
                brot++;
            }
        }
        return Math.min(trot,brot);
    }

}
