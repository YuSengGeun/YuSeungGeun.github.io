# FFT 알고리즘이란?
FFT(Fast Fourier Transform) 알고리즘은 이산 푸리에 변환(DFT, Discrete Fourier Transform)을 빠르게 계산하는 알고리즘입니다. DFT는 주어진 시계열 데이터의 주파수 성분을 분석하는 데 사용됩니다. 하지만 DFT는 계산 복잡도가 O(N^2)이므로 시계열 데이터의 크기가 커질수록 계산 시간이 길어지는 문제가 있습니다. 이에 대한 대안으로 개발된 것이 FFT 알고리즘으로, FFT는 DFT 계산 시간을 O(N log N)으로 줄일 수 있습니다. FFT 알고리즘은 분할 정복(divide-and-conquer) 방법을 사용하여 구현됩니다. 입력 시계열 데이터를 반으로 나눈 후, 재귀적으로 FFT를 계산하고 이를 조합하여 최종 FFT를 계산합니다.

# FFT 알고리즘의 구현
FFT 알고리즘은 여러 가지 방법으로 구현될 수 있습니다. 여기서는 가장 일반적인 Cooley-Tukey 알고리즘을 사용한 구현 방법을 설명하겠습니다. Cooley-Tukey 알고리즘은 다음과 같은 순서로 FFT를 계산합니다. 
1. 입력 신호를 짝수 인덱스와 홀수 인덱스를 갖는 두 부분으로 나눕니다. 
2. 각 부분에 대해 재귀적으로 FFT를 계산합니다. 
3. 계산된 FFT를 조합하여 전체 FFT를 계산합니다. 

여기서는 Java 언어를 사용하여 FFT 알고리즘을 구현해보겠습니다.
public class FFT {

    // 복소수 클래스
    static class Complex {
        double real, imag;

        public Complex(double real, double imag) {
            this.real = real;
            this.imag = imag;
        }

        public Complex add(Complex c) {
            return new Complex(real + c.real, imag + c.imag);
        }

        public Complex sub(Complex c) {
            return new Complex(real - c.real, imag - c.imag);
        }

        public Complex mul(Complex c) {
            return new Complex(real * c.real - imag * c.imag, real * c.imag + imag * c.real);
        }
    }

    // FFT 계산 함수
    public static Complex[] fft(Complex[] a, int n) {
        if (n == 1) return new Complex[] { a[0] };

        Complex[] even = new Complex[n / 2];
        Complex[] odd = new Complex[n / 2];

        for (int i = 0; i < n / 2; i++) {
            even[i] = a[2 * i];
            odd[i] = a[2 * i + 1];
        }

        Complex[] q = fft(even, n / 2);
        Complex[] r = fft(odd, n / 2);

        Complex[] y = new Complex[n];
        for (int k = 0; k < n / 2; k++) {
            Complex w = new Complex(Math.cos(2 * Math.PI * k / n), Math.sin(2 * Math.PI * k / n));
            y[k] = q[k].add(w.mul(r[k]));
            y[k + n / 2] = q[k].sub(w.mul(r[k]));
        }

        return y;
    }

    public static void main(String[] args) {
        // 테스트용 입력 데이터
        Complex[] a = { new Complex(1, 0), new Complex(2, 0), new Complex(3, 0), new Complex(4, 0) };

        // FFT 계산
        Complex[] y = fft(a, a.length);

        // 결과 출력
        for (Complex c : y) {
            System.out.println(c.real + " + " + c.imag + "i");
        }
    }
}
