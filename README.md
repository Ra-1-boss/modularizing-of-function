# modularizing-of-function
def find_root_bounds(x, power):
    """x a float, power a positive int
    return low, high such that low**power <=x and high**power >= x
    """
    low = min(-1, x)
    high = max(1, x)
    return low, high

def bisection_solve(x, power, epsilon, low, high):
    """x, epsilon, low, high are floats
    epsilon > 0
    low <= high and there is an ans between low and high s.t.
    ans**power is within epsilon of x
    returns ans s.t. ans**power within epsilon of x"""
    ans = (high + low)/2
    while abs(ans**power - x) >= epsilon:
        if ans**power < x:
            low = ans
        else:
            high = ans
        ans = (high + low)/2
    return ans

def find_root(x, power, epsilon):
    """Assumes x and epsilon int or float, power an int,
    epsilon > 0 & power >= 1
    Returns float y such that y**power is within epsilon of x.
    If such a float does not exist, it returns None"""
    if x < 0 and power%2 == 0:
        return None  # Negative number has no even-powered roots
    low, high = find_root_bounds(x, power)
    return bisection_solve(x, power, epsilon, low, high)


# Example usage
if __name__ == "__main__":
    # Test cases
    test_cases = [
        (25, 2, 0.001),    # Square root of 25
        (-27, 3, 0.0001),  # Cube root of -27
        (16, 4, 0.01),     # 4th root of 16
        (-16, 4, 0.01),    # Even root of negative number (should return None)
        (0.5, 3, 0.00001)  # Cube root of 0.5
    ]

    for x, power, epsilon in test_cases:
        result = find_root(x, power, epsilon)
        if result is None:
            print(f"No {power}th root exists for {x}")
        else:
            print(f"The {power}th root of {x} is approximately {result:.6f} (error < {epsilon})")
