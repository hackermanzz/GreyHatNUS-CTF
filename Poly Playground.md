

### Challenge

Poly playground is a straight-forward challenge that presents players with roots and in turn ask for the coefficients of said equation. There are several rules as dictated by the prompt.
1. Assume that repeated roots can be given.
2. Submit your answer as coefficients of your polynomial.
3. First coefficient should always be of the highest order. (Always 1)

![1](https://github.com/hackermanzz/GreyHatNUS-CTF/assets/55987051/b0fd7c41-c3e6-4efe-af03-10da8558b034)

The first few questions are simple as the resulting equations are easy to calculate by hand. But the game continues it presents the player with 3 roots or more. Futhermore, the time given to solve each question gets lesser and lesser, this means we have no choice but to script our answer

![2](https://github.com/hackermanzz/GreyHatNUS-CTF/assets/55987051/cc11cfe8-0899-437e-98a2-8f457382613d)

### Solution

We will be using python alongside the pwntools library to solve this challenge. First, lets create a function to process the data sent to us by the server.

```
def handle_data(data, conn):
    match = re.search(r"Roots:\s*(-?[0-9]+(?:,-?[0-9]+)*)", data)
    
    if match:
        roots = match.group(1).split(",")
        coefficients = construct_polynomial(roots)
        response = ",".join(map(str, coefficients))
        return response
    else:
        return "No match found. Waiting for more data..."
```

Let's walk through this function together. First, we utilize regular expressions to extract the values from the server's prompt, specifically targeting the ones following the `'Roots: '` prompt. We can use a capture group, denoted by round brackets, to capture these values. 

If the pattern is successfully found and the values are captured, we split the captured string using the delimiter `,` to obtain the values needed to construct our polynomial. With these values in hand, we proceed to create our polynomial. 

Given that Python lacks native support for mathematical symbols, we turn to the `sympy` library to assist us. 

```
def construct_polynomial(roots):
    x = Symbol("x")
    polynomial = 1
    for root in roots:
        polynomial *= x - float(root)
	polynomial_expanded = expand(polynomial)
    simplified_polynomial = simplify(polynomial_expanded)
    coefficients = [
        int(simplified_polynomial.coeff(x, i)) for i in range(len(roots), -1, -1)
    ]

    return coefficients
```

We begin by initializing a symbolic variable `x`, which serves as a placeholder for the variable in our polynomial expression. Then, we create a variable named `polynomial` to accumulate the polynomial expression incrementally. The subsequent for loop iterates through the list of roots provided as input. Within this loop, each root is subtracted from `x`, representing a linear factor of the polynomial. After the loop completes, the polynomial expression is expanded to remove any parentheses and simplify the expression. Following this expansion, the polynomial is further simplified using the `simplify` method to reduce it to its simplest form.

Subsequently, the coefficients of the polynomial are extracted. This is achieved by iterating over the powers of `x` in the simplified polynomial expression, beginning with the highest power (the degree of the polynomial) and progressing downward to the constant term. The `simplified_polynomial.coeff(x, i)` method is employed to obtain the coefficient of `x` raised to the power `i`. These coefficients are then converted to integers and collected into a list, which is subsequently returned to the main function for further processing or transmission back to the server.

A few touch ups and a `main` function to facilitate connections and data transfer between our client and server and our code should look something like this:

```
from pwn import *
import re
from sympy import Symbol, expand, simplify
import time


def construct_polynomial(roots):
    x = Symbol("x")
    polynomial = 1
    for root in roots:
        polynomial *= x - float(root)  # Convert root to float
    polynomial_expanded = expand(polynomial)
    simplified_polynomial = simplify(polynomial_expanded)
    coefficients = [
        int(simplified_polynomial.coeff(x, i)) for i in range(len(roots), -1, -1)
    ]
    return coefficients


def handle_data(data, conn):
    match = re.search(r"Roots:\s*(-?[0-9]+(?:,-?[0-9]+)*)", data)
    if match:

        roots = match.group(1).split(",")
        coefficients = construct_polynomial(roots)
        response = ",".join(map(str, coefficients))
        return response
    else:
        return "No match found. Waiting for more data..."


def main():
    host = "challs.nusgreyhats.org"
    port = 31113

    try:
        conn = remote(host, port)
        print("Connected to", host, "on port", port)

        while True:
            data = conn.recv().decode().strip()
            print("Received:", data)

            response = handle_data(data, conn)

            conn.sendline(response.encode().strip())
            print("Sent:", response)

    except Exception as e:
        print("Error:", e)

    finally:
        conn.close()


if __name__ == "__main__":
    main()

```

As the script continues to run, we can see that it was the right choice to script our answer rather than manually calculate them. There were a total of 100 questions?! Phew... lucky us, found the flag! 

![3](https://github.com/hackermanzz/GreyHatNUS-CTF/assets/55987051/ceb6de79-d4e1-4fb9-bd13-a04299404be7)


### Learning Points

This challenge teaches players on leveraging basic scripting and libraries to apply mathematical concepts effectively. It involves constructing polynomials, necessitating comprehension of roots and coefficients. Additionally, it educates players on establishing a client-server connection using pwntools.
