```
import numpy as np
import numpy.linalg as linalg

def zpca(A):
# sample matrix
# A = np.array([[120, 125, 125, 135, 145],
    # [61, 60, 64, 68, 72]])
    N = A.shape[1]
    # norm A
    M = A.sum(1)/N
    B = A - np.tile(M, (N, 1)).T
    # construct F
    F = B.T / np.sqrt(N-1)
    # covariance matrix
    S = np.dot(F.T, F)
    # SVD F
    U, E, V = linalg.svd(F)
    # eigenvalue of S
    E = E**2
    # eigenvector of S
    V = V.T
    return E, V

```
