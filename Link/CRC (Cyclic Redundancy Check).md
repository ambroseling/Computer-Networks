Error detection
- error detection and correction bits
Data:
- data protected by error checking, may include header fields

We choose $r$ CRC bits, R, such that $<D,R>$ exactly divisible by G (mod 2)

Steps
1) Find the generator $G(x)$
2) Shift the information by $k$ where $k$ is the highest order in the generator polynomial
3) do the long division on the shifted information polynomial with the generator polynomial
4) the remainder will tell you which bits are 1 to be appended to the data

#### Shift Register Implementation 
- Steps
	- 1) Accept information bits $i_{k-1}, i_{k-2},\cdots,i_2,i_1,i_0$
	- 2) Append $n-k$ zeros to the information bits
	- 3) feed sequence to a shift register circuit that performs polynomial division
	- 4) After $n$ shifts, the shift register contains the remainder


![[Screenshot 2025-04-10 at 4.25.56 PM.png]]


#### Primitive Polynomial 
- a polynomial of order $m$ is a primitive polynomial if the smallest positive integer $n$ such that $g(x)$ divides $(x^n + 1)$ is $n = 2^{m}-1$, $m$ is the order of the generator
- if your generator polynomial can divide $(x^{n}+1)$ evenly and $n$ is $2^{m}-1$, then its a primitive polynomial


#### Summary of Error Detection Requirements
Assume: $n$ : number of data bits, $m$: order of generator
- 1 bit error $\rightarrow$
	- Error form: $e(x) = x^n$ (we want $g(x)$ to not divide this)
	- generator has a constant value of 1, not divisible by $x$
- 2 bit error $\rightarrow$ 
	- Error form: $e(x) = x^k(x^n + 1)$ (we want $g(x)$ to not divide this)
	- if the generator polynomial is primitive of order $m$ and if the bits are at most separated at most $n$ bits apart ($n \lt 2^m -1$)
- Odd number of error $\rightarrow$ 
	- if the polynomial has the term $(x+1)$ it is detectable
- Burst of errors $\rightarrow$
	- if generator has degree $m$ and $e(x) = x^i p(x)$ where degree of $p(x)$ = $k \lt m$, error can be detected






