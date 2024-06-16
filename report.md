# 实验作业标题
- **姓名： 学号： 得分：**


## 目标
太阳黑子日变化的综合分析

## 分析
本实验旨在通过对太阳黑子日变化数据的分析，增强学生对数据处理、可视化及分析技能的掌握，并了解太阳活动对地球气候和通讯系统的影响。我们利用Python编程语言，采用了多种方法对太阳黑子数据进行了深入分析，包括绘制逐日变化图、计算滑动平均、傅立叶变换、小波变换以及ARIMA预测模型。

## 程序与说明

'''

    # 安装所需的库
    try:
        import numpy as np
        import pandas as pd
        import matplotlib.pyplot as plt
        from scipy.fft import fft, fftfreq
        import pywt
        from statsmodels.tsa.arima.model import ARIMA
    except ImportError as e:
        import os
        os.system('pip install numpy pandas matplotlib scipy PyWavelets statsmodels')
        import numpy as np
        import pandas as pd
        import matplotlib.pyplot as plt
        from scipy.fft import fft, fftfreq
        import pywt
        from statsmodels.tsa.arima.model import ARIMA

    # 读取数据
    data = pd.read_csv('E:\money\\2\sunspot\\SN_d_tot_V2.0.txt',        
    delim_whitespace=True, header=None,
                    names=['Year', 'Month', 'Day', 'Decimal_date', 'Sunspot_number', 
                    'Std_dev', 'Num_obs', 'Definitive'])

    # 删除缺失值和异常值
    data = data[data['Sunspot_number'] >= 0]

    # 提取需要的列
    dates = data['Decimal_date']
    sunspots = data['Sunspot_number']
    errors = data['Std_dev']

    # 绘制逐日变化图
    plt.figure(figsize=(10, 5))
    plt.errorbar(dates, sunspots, yerr=errors, fmt='.', color='b', ecolor='r', 
    capsize=5)
    plt.xlabel('Decimal Date')
    plt.ylabel('Sunspot Number')
    plt.title('Daily Sunspot Numbers with Error Bars')
    plt.grid(True)
    plt.show()

    # 计算30天滑动平均
    sunspots_30d_avg = sunspots.rolling(window=30).mean()

    # 绘制30天滑动平均图
    plt.figure(figsize=(10, 5))
    plt.plot(dates, sunspots_30d_avg, color='g')
    plt.xlabel('Decimal Date')
    plt.ylabel('30-Day Moving Average Sunspot Number')
    plt.title('30-Day Moving Average of Sunspot Numbers')
    plt.grid(True)
    plt.show()

    # 傅立叶变换
    N = len(sunspots)
    T = 1.0  # 采样间隔为1天
    yf = fft(sunspots)
    xf = fftfreq(N, T)[:N//2]

    plt.figure(figsize=(10, 5))
    plt.plot(xf, 2.0/N * np.abs(yf[:N//2]))
    plt.grid()
    plt.xlabel('Frequency (1/days)')
    plt.ylabel('Amplitude')
    plt.title('Fourier Transform - Sunspot Numbers')
    plt.show()

    # 小波变换
    scales = np.arange(1, 128)
    coeffs, freqs = pywt.cwt(sunspots, scales, 'morl')

    plt.figure(figsize=(10, 5))
    plt.imshow(np.abs(coeffs), extent=[min(dates), max(dates), min(freqs), 
    max(freqs)], cmap='jet', aspect='auto')
    plt.colorbar(label='Magnitude')
    plt.xlabel('Date')
    plt.ylabel('Frequency (1/days)')
    plt.title('Continuous Wavelet Transform - Sunspot Numbers')
    plt.show()

    # ARIMA预测模型
    # 使用月平均（Monthly Average）平滑数据，观察长期趋势和周期
    monthly_data = data.groupby(['Year', 'Month']) 
    ['Sunspot_number'].mean().reset_index()

    # 将 Year 和 Month 转换为 datetime 格式
    monthly_data['Date'] = pd.to_datetime(monthly_data[['Year', 
    'Month']].assign(DAY=1))

    # 设置日期为索引
    monthly_data.set_index('Date', inplace=True)

    # 拟合 ARIMA 模型
    model = ARIMA(monthly_data['Sunspot_number'], order=(5, 1, 0))
    model_fit = model.fit()

    # 预测未来 10 年（120 个月）
    forecast = model_fit.forecast(steps=120)

    # 绘制预测结果
    plt.figure(figsize=(10, 5))
    current_date = pd.to_datetime('now')
    # 构建预测时间范围
    future_dates = pd.date_range(start=current_date, periods=121, freq='M')[1:]

    plt.plot(future_dates, forecast, label='Forecast', color='red')
    plt.xlabel('Date')
    plt.ylabel('Sunspot Number')
    plt.title('Sunspot Number Forecast for the Next 10 Years')
    plt.legend()
    plt.grid(True)
    plt.show() 
    
'''


## 结果与讨论

1. 逐日变化图
![alt text](Figure_1.png)
描述: 该图展示了太阳黑子数随时间的逐日变化，并附带误差条。
分析: 从图中可以观察到太阳黑子数存在明显的周期性波动，且数值在不同年份间有显著差异。

2. 30天滑动平均图
![alt text](Figure_2.png)
描述: 该图展示了太阳黑子数的30天滑动平均值。
分析: 滑动平均图平滑了数据中的短期波动，更清晰地展现了太阳黑子的长期变化趋势。可以看出，太阳黑子的活动周期大约为11年，这与太阳活动周期一致。

3. 傅立叶变换
![alt text](Figure_3.png)
描述: 通过傅立叶变换，我们将太阳黑子数的时间序列转换到频率域，以观察其频谱特性。

4. 小波变换
![alt text](Figure_4.png)
描述: 小波变换提供了时间-频率域的分析结果，可以同时观察到太阳黑子数随时间的频率变化。
分析: 小波变换图显示了不同时间段内太阳黑子的频率特性。通过该图，我们可以更细致地分析短期和长期的周期变化。

5. ARIMA预测模型
![alt text](Figure_5.png)
描述: 使用ARIMA模型对太阳黑子数进行了预测，以估计未来10年的变化情况。

## 总结
本实验通过多种数据分析和可视化技术，对太阳黑子数的日变化进行了详细研究。我们采用了滑动平均、傅立叶变换和小波变换等方法，从不同角度分析了太阳黑子的变化规律，并通过ARIMA模型对未来的太阳黑子数进行了预测。实验结果表明，太阳黑子数存在显著的周期性波动，其活动周期大约为11年，这与太阳活动周期相一致。通过本实验，学生不仅掌握了数据分析和可视化的基本技能，还深入了解了太阳活动对地球的影响及其周期性变化规律。未来的研究可以进一步优化模型，提升预测的准确性，并结合其他太阳活动数据进行综合分析。

## 参考文献
'''
@misc{sidc,
  author       = {{SIDC}},
  title        = {SILSO Data Files},
  howpublished = {Royal Observatory of Belgium},
  year         = {Accessed: 16 June 2024},
  url          = {https://www.sidc.be/SILSO/datafiles}
}

'''

