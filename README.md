# Stick-Pair-Divisor-Count

In a crafty village, Ravi discovered N sticks, each with a unique length denoted by Aᵢ. He learned that each stick could be shortened to any length Y as long as Aᵢ % Y == 0. This meant that a stick of length Aᵢ could be burnt to X different lengths, where X is the count of divisors of Aᵢ. Curious about the sticks, Ravi decided to find the total number of unordered pairs of sticks that had the same X value. Can you help Ravi determine the number of such pairs?

def stick_pair_divisor_count(N, A):
    # Step 1: Precompute divisor counts for all numbers up to 10^6
    MAX_VAL = 10**6
    divisor_count = [0] * (MAX_VAL + 1)
    
    for i in range(1, MAX_VAL + 1):
        for j in range(i, MAX_VAL + 1, i):
            divisor_count[j] += 1

    # Step 2: Group stick lengths by their divisor count
    groups = {}
    for stick in A:
        x = divisor_count[stick]
        if x not in groups:
            groups[x] = 0
        groups[x] += 1

    # Step 3: Count pairs in each group
    total_pairs = 0
    for count in groups.values():
        if count > 1:
            total_pairs += count * (count - 1) // 2

    return total_pairs

# Input
N = int(input())
A = list(map(int, input().split()))

# Output the result
print(stick_pair_divisor_count(N, A))
