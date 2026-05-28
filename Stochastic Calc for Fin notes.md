Stochastic Calculus for Finance 1 (The Binomal Asset Pricing Model) by Steven Shreve

PAGE LAST READ: 41 (1.6-1.1)

Table of Contents:
    1. Binomial No-Arb Pricing Model
        1.1 One-Period 1.2 Multi-Period 1.3 Computational Considerations 1.4 Summary 1.5 Notes 1.6 Excerices
    2. Probability Theory on Coin Toss Space
    3. State Prices
    4. American Derivative Securities
    5. Random Walk
    6. Interest-Rate-Dependent Assets

Textbook Extra Information:
    Chapters 1-3 are important foundational concepts for modern quant finance
    4-6 investigate more specific circiumstances that arrive in finance

    Volume II is self contained but it seems like atleast chapters 1-3 of Vol 1 are important







NOTES

1.1 (One Period Binomial Model)
    u (up factor) multiplied by S0 to get uS0 = S1(H)
    d (down factor) multiplied by S0 to get dS0 = S1(T)

    Define Arbitrage: Start with $0, can't lose, possible to win
    To rule out arbitrage we must assume 0 < d < 1 + r < u  (1.1.2) (Common to have d = 1/u, not necessary)

    Example:
        S(0) = 4, u = 2, d = 1/2, r=1/4 (pretend there exists a european option with strik=5 and premium=1.2 that expires at time 1)
        We can replicate this by using our $1.20 + $.80 debt to get $2 -> 1/2 share
        At time 1 our debt is worth $1 since .80*1.25 = 1. 
        We either have 1/2($8 share) - 1 debt = 3 or 1/2($2 share) - 1 debt = 0.
        Thus, the price of the option must also be $1.20 because the value of an option with strike 5 is 3 or 0 depending 1 u or d movement from S0

    Idea:
        To replicate the price of a derivative security we replicate as above
        We begin with wealth X0 and buy q0 shares, thus our cash position at T=0 is X0 - q0*S0 (initial wealth - quantity * share price, all at T=0)
        We also have a borrowing/lending rate of r, where 1+r is the multiplier over a period 1
        Our wealth at T=1; X1, is q0*S1 + (1+r)(X0 - q0*s0), where the right hand side is negative since our cash position at T0 is negative
        We need this to be equivalent for both our up and down scenarios compared to our option

        Value of option vs value of hedging position:
            X0 + q0(1/(1+r) * S1H - S0) = (1/(1+r)) * V1H (Value of Hedge port with up move is the same as value of option discounted)
            Same applies for down

    Big Takeaway:
        We can offer a closed form solution given we know what r, u, and d are
        p = (1 + r - d) / (u-d) and q = 1 - p = (u - 1 - r) / (u - d)
        Once we know q and p, we can solve for q0 (quantities of shares at 0)
        q = (V1H - V1T) / (S1H - S1T) Where V represents the value of the option at H and T, S1H is value of asset at u...

        Value of option at T0 = value of option at up * prob up + value of option at down * prob down

        Because no arbitrage assumes drift lower than actual, the following prevails
        S0 < the discounted value of both option outcomes * their probabilities 
        (This is because investors need a premium to assume security risk, where no-arb assumes risk-neutral/no extra risk when buying option)

        THIS MEANS RISK-NEUTRAL ASSUMES: DRIFT = MONEY MARKET
        IN REALITY DRIFT > MONEY MARKET (RF - Div)

1.2 (Multiperiod Binomial Model)
    We continue the u and d assumptions with a given r for multiple "coin flips"

    X (wealth of hedging portfolio), V (Value of option), and q (quantity of shares to hedge)
    Are all related over every time-period and coin-flip path available

    X,V,q are all stochastic processes, meaning a sequence of random variables indexed by time.
    They are random because they depend on the coin tosses

    wealth equation: Xn+1 = qn * Sn+1 + (1+r)(Xn - qn*Sn)
    assuming we know qn, r, and the prices after 1 u or d, we can know X at the next flip for both scenarios

    V0 is the value of X0 that accomplishes a satisfactory replication of the european option

    To completely establish arbitrage, one must be readjusting the hedge after every flip

    We can also use the known values of the option price at all scenarios at time N in order to know the price of the option at time n.
    You can walk backwards because you already know the path that has been taken at every time.
    In order to replicate the option with a portfolio of stock and money market, you can follow the princinples above to calculate an appropriate share price and money market value for each path. 

    Note that if you know the price/payout of the option at time N, this can be used to identify X, and furthermore to identify q, which leaves you with the remaining variable of the $ in money market which completes the hedging portfolio.

1.3 (Computational Considerations)
    Computing all binomial paths for 100 periods leaves us with 2^100 paths (Vn)
    If we compute all possible final share prices, we only have 101 (vn)
    This is because we can denote the stock price by just the # of ups, or # of downs
    Given 100 flips, there are only 101 possibilities for the # of ups (0 - 100)
    This greatly reduced computational complexity

    Using methods from 1.1 and 1.2, instead of calculating our X, V, and q using the path that was taken, we can use the price of the underlying instead, reducing possible options to compute


1.4 (Summary)
    We are evaluating share prices and related options where - 
    An asset starts at S0, is then *u or *d for each step, resulting in 2^n paths with n+1 end prices. There is a given rf = r which is per period interest for the MM
    0 < d < 1+r < u in our model for no arbitrage (MUST FOR THE MDOEL)

1.5 (Notes)
    No-arb pricing is implicit in Black-Scholes-Merton

1.6 (Exercises)
    1. Assume a 1 period binomial market where u and d are both positive probability and probabilities sum to 1. Show that if X0 = 0 then we cannot have X1 with positive probability without also negative probability

    Assume X1 = q0S1 + (1+r)(X0 - q0S0) 
    Where X = wealth of portfolio, q = quantity of shares, s = price, r = rf rate, and the numbers relate to time either 0 or 1

        Start with equation: X1 = q0S1 + (1+r)(X0 - q0S0), lets say a = q0
        then X1 = aS1 + (1+r)(X0 - aS0). Lets say b = u or d, whichever was chosen
        then X1 = aS0*b + (1+r)(0 - aS0)
        then X1 = a(S0*b + (1+r)(-S0))
        X1 = a*S0(b -(1+r)) lets say a*S0 is z
        X1 = z(b - (1 + r)
        We know if b is u, u > (1+r) and if b is d, d < (1+r), so the sign flips given u or d for b if both u and d are positive values
         


2.1 (Finite Probability Spaces)
    A finite probability space has p, a probability, w, an event, and omega, a sample space. The sum of all p(w)'s = 1, where omega contains all possible outcomes.

    Omega is nice because it contains a finite amount of unique events.
    This allows P(A u B) = P(A) + P(B) and so forth.

2.2 (Random Variables, Distributions, Expectations)
    A random expirement generally generates numerical data. This gives rise to the concept of a random variable.

    Distribution defines the probability of random variables.
    The random variable is a functioned defined on omega, its distribution is a tabulation of probabilities that the random variables takes various values.

    E[X] = sum( X(w) * P(w) )
    This means the expectation is the sum of the possible outcomes (random variable) * the probability of those outcomes happening (distribution)

    Jensens inequality:
    The function of an average is less than or equal to the average of a function.
    E[(X^2)] >= (E[X])^2 
    On the right side, the function is u^2, where u is the average (E[X])
    On the left side, the average is of the funcion, E[(X^2)]
    Jensens inequality states the left side is always >= right side

2.3 (Conditional Expectations)
    Now lets think again of our binomial model we use in chapter 1
    Where you have p and q which represent the probabilities of u and d
    where (p*u + q*d)/(1+r) = 1 ; Meaning the average return of the next step is equal to the risk free rate, and the average next price discounted by the risk free rate to the current price is always equal

    Constants and known values can be taken in or out of an expectation
    Random variables in the future can be taken out as well, as they do not add any information.

    A known interest rate can be taken out of the expectation.
    An unknown interest rate (random variable) must be kept in

2.4 (Martingales)
    Processes that make the value S at time n+1 (Sn+1) equivalent to the value S at time n multiplied by the risk free rate (or make the value at time n the discounted value of n+1) are called martingales.

    A martingale is when the value at time n is EQUAL to the expectation of value at time n+1

    A submartingale is when it is less than or equal
    A supermartingale is when it is greater than or equal

    For a binomial asset pricing model, the idea is that our present value is always equal to the expectation of value at any future m that is in between n and N.

    The expectations of value at each time n are the same. But only the true value of M0 is = EM0, since any true value M after that is random.

    In a martingale binomial model where u=2 and d=0.5, p=1/3 and q=2/3
    This is because the expectation of value at t=n+1 is the same as t=n

    In reality the expectation of the rise in value at t=n+1 must be greater than the money market in order to compensate investors for risk.

    This makes the discounted stock price a submartingale, as the value at t=n is less than the expectation of value at t=n+1.

    In risk-neautral scenario the discounted stock price is a martingale, as the price expectation only moves upwards at the same rate as rf/money market

    First Fundemental Theorem of Asset Pricing:
        Find a risk-neutral measure: p,q,u,d such that the discounted value of all future values is equal

2.5 (Markov Processes)
    If we have a binomial model from n to N, with Xn being a variable and we have two functions f(x) and g(x)
    And E[f(Xn+1)] = G(Xn) : This is a markov process

    The binomial asset pricing model that models an asset price using:
    u,d,p,q is a markov process, as our price at n X, relates to our price at n+1 g(X) where g(x) = X * (p*u + u*d)/(1+r)

    A martingale is such that f(x) and g(x) are equal
    if pu*qd = 1 then it is martingale, but a binomial model is always markov

2.6 (Summary)
    Markov means you don't need any information of how you got to time n, other than the random variables that are apart of your markov process

    This is why to achieve a markov process that uses the max value of a security, we must include the current asset of the security, as this is a proxy for the path that the asset price is taken.
    The exact path does not matter, but we do need to know the current price to understand how to estimate the max of the asset price in the future.

