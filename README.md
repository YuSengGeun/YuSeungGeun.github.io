# FFT 알고리즘이란?
FFT(Fast Fourier Transform) 알고리즘은 이산 푸리에 변환(DFT, Discrete Fourier Transform)을 빠르게 계산하는 알고리즘입니다. DFT는 주어진 시계열 데이터의 주파수 성분을 분석하는 데 사용됩니다. 하지만 DFT는 계산 복잡도가 O(N^2)이므로 시계열 데이터의 크기가 커질수록 계산 시간이 길어지는 문제가 있습니다. 이에 대한 대안으로 개발된 것이 FFT 알고리즘으로, FFT는 DFT 계산 시간을 O(N log N)으로 줄일 수 있습니다. FFT 알고리즘은 분할 정복(divide-and-conquer) 방법을 사용하여 구현됩니다. 입력 시계열 데이터를 반으로 나눈 후, 재귀적으로 FFT를 계산하고 이를 조합하여 최종 FFT를 계산합니다.
