# EXP.NO.10-Simulation-of-Error-Detection-and-Correction-Algorithms
10.Simulation of Error Detecion and Correction Algorithms

# AIM
To simulate error detection and correction techniques, such as Parity Check and Hamming Code, and to understand their working principles using Python programming.

# SOFTWARE REQUIRED
Python-colab

# ALGORITHMS
Parity Check (Error Detection) Count the number of 1’s in the data.

Add a parity bit to make the total number of 1’s even (even parity) or odd (odd parity) At the receiver, recount the 1’s to detect any error.

Hamming Code (Error Detection and Correction) Insert parity bits at positions that are powers of 2 (1, 2, 4, etc.).

Calculate each parity bit based on a specific set of data bits.

At the receiver, recompute parity to find the error position.

# PROGRAM
``` python
import numpy as np

pb = []           # Parity matrix rows
Ik = []           # Identity matrix
p = []
m = []
h_dis = []
r_code = []
err = []


col = int(input("Enter the number of parity bits: "))
row = int(input("Enter the number of message bits: "))

print("\nEnter the parity matrix rows:")
for i in range(row):
    p = list(map(int, input(f"Row {i+1}: ").split()))
    if len(p) != col:
        raise ValueError(f"Each row must have {col} elements.")
    pb.append(p)


p_mat = np.array(pb, dtype=int)
Ik = np.eye(row, dtype=int)


g_mat = np.hstack((Ik, p_mat))

k = g_mat.shape[0]
n = g_mat.shape[1]


m = np.array([[1 if (i >> (k - j - 1)) & 1 else 0 for j in range(k)] for i in range(2 ** k)])


c = np.mod(np.dot(m, g_mat), 2)

