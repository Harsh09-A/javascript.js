# javascript.js
j.s code
1.
  function minimumPlanesRequired(arr) {
  const n = arr.length;
  const dp = new Array(n).fill(Infinity);
  dp[0] = 0;
  for (let i = 0; i < n; i++) {
    for (let j = i + 1; j <= i + arr[i] && j < n; j++) {
      dp[j] = Math.min(dp[j], dp[i] + 1);
    }
  }
  return dp[n - 1] === Infinity ? -1 : dp[n - 1];
}


const arr = [2, 1, 2, 3, 1];
console.log(minimumPlanesRequired(arr)); 

n is the length of the input array arr.
dp is an array of length n where dp[i] represents the minimum number of planes required to reach airport i from airport 1.
Initialize dp[0] to 0 since we are already at the starting airport.
For each airport i, we check all possible destinations j that can be reached from i with the available fuel. If dp[j] can be updated to a smaller value by taking a flight from i to j, we update it accordingly.
After iterating through all airports, dp[n - 1] will contain the minimum number of planes required to reach the last airport. If it is still infinity, it means we couldn't reach the last airport and we return -1.
Note that this solution has a time complexity of O(n^2) and a space complexity of O(n). It can be optimized further using a BFS approach or by using a priority queue to store the next possible destinations.

2.
  function minimumPlanesRequired(fuelArr) {
  const N = fuelArr.length;
  let currentPos = 0;
  let planesHired = 0;

  while (currentPos < N - 1) {
  
    if (fuelArr[currentPos] === 0) {
      return -1;
    }

   
    let maxFuel = 0;
    let maxFuelIndex = 0;
    for (let i = currentPos + 1; i <= Math.min(currentPos + fuelArr[currentPos], N - 1); i++) {
      if (fuelArr[i] > maxFuel) {
        maxFuel = fuelArr[i];
        maxFuelIndex = i;
      }
    }

    if (maxFuel === 0) {
      return -1;
    }

    currentPos = maxFuelIndex;
    planesHired++;
  }

  return planesHired;
}

const arr = [1, 6, 3, 4, 5, 0, 0, 0, 6];
const minPlanes = minimumPlanesRequired(arr);
console.log(minPlanes); 

Initialize a variable currentPos to 0 (i.e., the starting airport).
Initialize a variable planesHired to 0.
While currentPos is less than N-1 (i.e., we haven't reached the last airport yet):
If the fuel at currentPos is 0, return -1 (we can't fly anywhere from here).
Find the index maxFuelIndex of the airport that we can reach from currentPos with the maximum fuel.
Set currentPos to maxFuelIndex.
Increment planesHired.
Return planesHired.

