Stochastic Calculus for Finance 1 (The Binomal Asset Pricing Model) by Steven Shreve

PAGE LAST READ: 8

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
        IN REALITY DRIFT > MONEY MARKET




