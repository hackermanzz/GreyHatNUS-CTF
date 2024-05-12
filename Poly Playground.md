
Poly playground is a straight-forward challenge that presents players with roots and

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