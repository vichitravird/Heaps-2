# Heaps-2

## Problem1: Top K Frequently Repeating Elements(https://leetcode.com/problems/top-k-frequent-elements/)

### Time Complexity: O(n)
### Space Complexity: O(n)

class Solution:
    def topKFrequent(self, nums: List[int], k: int) -> List[int]:
        hashMap = {}
        for num in nums:
            hashMap[num] = hashMap.get(num, 0) + 1
        #using heap sort nlogk
        #use minheap, sort by value, when heap size greater than k, pop the min element
        # pq = []
        # for key,v in hashMap.items():
        #     heapq.heappush(pq, (v,key))
        #     if len(pq)>k:
        #         heapq.heappop(pq)
        # result = []
        # #In the end we have top k frequent elements
        # while len(pq) > 0:
        #     val = heapq.heappop(pq)
        #     result.append(val[1])

        #using bucketsort #O(n)
        freqMap = {}
        minVal, maxVal = 1e9,-1e9
        #create buckets and enter nums with buckets
        #also maintain a max and min for bucketlimits
        for num in hashMap:
            val = hashMap.get(num)
            if val not in freqMap:
                freqMap[val] = []
            vals = freqMap[val]
            vals.append(num)
            minVal = min(minVal, val)
            maxVal = max(maxVal, val)
        
        result = []
        j = 0
        #Iterate the buckets from max to min because we want top k frequent elements
        #append the nums in the bucket to result until result size equals k then return result
        for i in range(maxVal, minVal-1, -1):
            if i in freqMap:
                for num in freqMap.get(i):
                    result.append(num)
                    j+=1
                    if j == k:
                        return result
        return result
