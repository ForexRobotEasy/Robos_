//+------------------------------------------------------------------+
//|                                                  Robos.mq5       |
//|                          Copyright 2021, Your Company Name       |
//|                                             https://www.yourwebsite.com |
//+------------------------------------------------------------------+
#property copyright 'Copyright 2021, Your Company Name'
#property link      'https://www.yourwebsite.com'
#property version   '1.0'

// Indicator parameters
input int OscillatorPeriod = 14; // Period for the multi-timeframe oscillator
input int OverboughtLevel = 70; // Level for extreme overbought condition
input int OversoldLevel = 30; // Level for extreme oversold condition

// Global variables
double OscillatorBuffer[]; // Buffer to store oscillator values

//+------------------------------------------------------------------+
//| Custom indicator initialization function                         |
//+------------------------------------------------------------------+
int OnInit()
{
    // Define indicator buffers
    SetIndexBuffer(0, OscillatorBuffer, INDICATOR_DATA);

    // Set indicator parameters
    SetIndexStyle(0, DRAW_LINE);
    SetIndexLabel(0, 'Oscillator');

    return(INIT_SUCCEEDED);
}

//+------------------------------------------------------------------+
//| Custom indicator iteration function                              |
//+------------------------------------------------------------------+
int OnCalculate(const int rates_total,
                const int prev_calculated,
                const datetime &time[],
                const double &open[],
                const double &high[],
                const double &low[],
                const double &close[],
                const long &tick_volume[],
                const long &volume[],
                const int &spread[])
{
    // Calculate oscillator values
    for(int i = rates_total - 1; i >= 0; i--)
    {
        OscillatorBuffer[i] = iCustom(_Symbol, _Period, 'YourOscillatorIndicator', OscillatorPeriod, i);
    }

    // Check for extreme overbought or oversold conditions
    if(OscillatorBuffer[0] >= OverboughtLevel)
    {
        // Generate alert for extreme overbought condition
        Alert('Extreme Overbought Condition!');
    }
    else if(OscillatorBuffer[0] <= OversoldLevel)
    {
        // Generate alert for extreme oversold condition
        Alert('Extreme Oversold Condition!');
    }

    // Generate trading signals
    if(OscillatorBuffer[0] > OscillatorBuffer[1] && OscillatorBuffer[1] <= OverboughtLevel)
    {
        // Generate signal for potential reversal or significant price movement
        // Place your trading logic here
    }

    return(rates_total);
}

//+------------------------------------------------------------------+
//| Additional Information                                           |
//+------------------------------------------------------------------+
//
// This code is a custom indicator for the MetaTrader 5 platform (MT5).
// It calculates a multi-timeframe oscillator and generates trading signals based on extreme overbought or oversold conditions.
// The indicator parameters can be adjusted to suit your trading strategy.
//
// To use this indicator, simply copy and paste the code into the MetaEditor in MT5, compile it, and attach it to a chart.
// You can adjust the indicator parameters in the input section of the code.
//
// This code is provided by Your Company Name and is for educational purposes only.
// It is not intended as financial advice or a recommendation to trade.
//
// For more information and updates on this code, please visit our website:
// https://forexroboteasy.com/forex-robot-review/robos-indicator-review-latest-version-4-0-download-now-for-real-results/
