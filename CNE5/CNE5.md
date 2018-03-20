

#CNE5

### Size

* LNCAP
* natural log of market cap



### Beta

* BETA
* $r_t-r_{ft} = \alpha +\beta R_t + e_t$
* $r_t - r_{ft}$ excess stock return
  * $r_t$ stock return
  * $r_{ft}$ risk-free return (0.04 / 国有债券)
* $Rt$ 
  * estimation universe
    * all A-shares
    * capture the underlying structure
  * the cap-weighted excess return of the estimation universe $R_t$
  * How to calculate (???)
    * A-shares universe stock return - risk-free return
    * universe return = each stock's return * cap-weight
* $\alpha$ , $\beta$ , $e_t$ : regression coefficients & residuals
* 252 trading days ; half-life 63 trading days
  * $x[:252] = R_t$ ,  $y[:252] = r_t - r_{ft}$
  * $ w = (\frac{1}{2})^{\frac{1}{63}}$
  * OLS : $\beta = \sum_ix_iy_i / \sum_ix_i^2$
  * Weighted-OLS : $\beta=\sum_iw^{252-i}x_iy_i/\sum_iw^{252-i}x_i^2$



### Momentum

* RSTR
* $RSTR = \sum_{t=L}^{T+L}w_t[ln(1+r_t)-ln(1+r_{ft})]$
  * trailing T = 504 days , lag L = 21 days
  * $r_t$ , $r_{ft}$
  *  $w_t = (\frac{1}{2})^{\frac{1}{126}}$



### Residual Volatility

* $0.74*DASTD + 0.16*CMRA + 0.10 * HSIGMA$
* DASTD
  * volatility of daily excess returns  $x[i] = ln(\frac{close}{preclose})$
  * past 252 trading days $x[:252]$
  * half-life of 42 trading days $w = (\frac{1}{2})^{\frac{1}{42}}$
  * $x[i] * w^{252-i}$  standard deviation
* CMRA
  * $Z_T=\sum_{t=1}^{T}[ln(1+r_t)-ln(1+r_{ft}))]  (T = 1, 2, ..., 12)$
  * $r_t , r_{ft}$ stock, risk-free return of month t
  * $CMRA = ln(1+Z_{max}) - ln(1+Z_{min})$
* HSIGMA
  * $\sigma = std(e_t)$  residuals in BETA
  * half-life of 63 trading days ; over 252 days
* orthogonalize with respect to BETA & SIZE



### Non-linear Size

* NLSIZE
* $LNCAP ^ 3$
* orthogonalize with respect to SIZE (on a regression-weighted basis ???)
* Winsorize 去极值化 "$3\sigma$"原则
* Standardize 标准化



###Book-to-Price

* BTOP
* book value / market capitalization  $\frac{1}{PB}$



### Liquidity

* $0.35*STOM+0.35*STOQ+0.30*STOA$
* STOM  (share turnover one month)
  * $STOM = ln(\sum_{t=1}^{21}\frac{V_t}{S_t})$
  * Vt 当日成交量  St 流通股总量
* STOQ (share turnover one quarter)
  * $STOQ = ln[\frac{1}{T}\sum_{t=1}^Texp(STOM_t)], T=3$
* STOA (share turnover one annual)
  * $STOQ = ln[\frac{1}{T}\sum_{t=1}^Texp(STOM_t)], T=12$



### Earnings Yield

* $0.68*EPFWD + 0.21*CETOP + 0.11 * ETOP$
* EPFWD
  * 未来12个月期望收益 / 当前市值
  * 未来12个月期望收益 = 分析师预测当年收益、下一年收益加权平均
* CETOP
  * 当前12个月内每股收益 / 当前股价
  * Cash EPS / price
* ETOP
  * 当前12个月内收益 / 当前市值
  * 收益 = 上一财年收益 + （当前中期报告 - 去年同时期中期报告）



### Growth

* $0.18*EGRLF+0.11*EGRSF+0.24*EGRO+0.47*SGRO$
* EGRLF：分析师预测长期收益率
* EGRSF：分析师预测短期收益率
* EGRO
  * 年报每股收益 线性回归 5个财年
  * EGRO = 斜率系数 / 平均收益
* SGRO
  * 年报每股销售额 线性回归 5个财年
  * SGRO = 斜率系数 / 平均销售额



### Leverage

* $0.38*MLEV + 0.35*DTOA+0.27*BLEV$
* MLEV
  * $MLEV = \frac{ME+PE+LD}{ME}$
  * ME 普通股市值 ； PE 优先股账面价值 ； LD  长期负债账面价值
* DTOA
  * $DTOA = \frac{TD}{TA}$
  * TD 所有债务账面价值 ； TA 总资产账面价值
* BLEV
  * $BLEV = \frac{BE+PE+LD}{BE}$
  * BE 普通股账面价值



####[Appendix] Orthogonalize



