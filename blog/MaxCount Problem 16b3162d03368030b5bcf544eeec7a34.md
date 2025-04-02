---
title:MaxCount Problem
date:2025-04-02
technology:["C++","algorithm"]
---

# MaxCount Problem

`#include <stdio.h>
#include <string.h>
#define MAX 1000

int max(int a, int b) {
    return a > b ? a : b;
}

int maxCount(int n) {
    // dp[i] represents maximum characters possible after i operations
    int dp[MAX] = {0};
    // Initial state: 0 characters at step 0
    dp[0] = 0;
    // Stores number of characters in clipboard
    int clipboard = 0;
    
    // Calculate from step 1 to n
    for(int i = 1; i <= n; i++) {
        // 1. Add a single character
        dp[i] = dp[i-1] + 1;
        // Check previous steps for optimal copy-paste combinations
        for(int j = 2; j < i; j++) {
            // Calculate total characters possible through copy-paste
            // dp[j-1] is characters before copy, (i-j) is possible paste operations
            int current = dp[j-1] * (i - j + 1);
            dp[i] = max(dp[i], current);
        }
    }
    return dp[n];
}

int main() {
    int n;
    scanf("%d", &n);
    printf("Maximum number of characters after %d operations: %d\n", n, maxCount(n));
    return 0;
}`