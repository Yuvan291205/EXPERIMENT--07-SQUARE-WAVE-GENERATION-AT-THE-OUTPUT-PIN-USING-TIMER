# EXPERIMENT-07: SQUARE WAVE GENERATION AT THE OUTPUT PIN USING TIMER

### Aim:
To generate a PWM wave at the timer pin output and  simuate it on  proteus using an virtual oscilloscope  

### Components required:
STM32 CUBE IDE, Proteus 8 simulator .

### Theory:

The timer modules can operate a variety of modes one of which is the PWM mode. Where the timer gets clocked from an internal source and counts up to the auto-reload register value, then the output channel pin is driven HIGH. And it remains until the timer counts reach the CCRx register value, the match event causes the output channel pin to be driven LOW. And it remains until the timer counts up to the auto-reload register value, and so on.

The resulting waveform is called PWM (pulse-width modulated) signal. Whose frequency is determined by the internal clock, the Prescaler, and the ARRx register. And its duty cycle is defined by the channel CCRx register value. The PWM doesn’t always have to be following this exact same procedure for PWM generation, however, it’s the very basic one and the easier to understand the concept. It’s called the up-counting PWM mode. We’ll discuss further advanced PWM generation techniques as we go on in this series of tutorials.

The following diagram shows you how the ARR value affects the period (frequency) of the PWM signal. And how the CCRx value affects the corresponding PWM signal’s duty cycle. And illustrates the whole process of PWM signal generation in the up-counting normal mode.

STM32 Timers – PWM Output Channels

Each Capture/Compare channel is built around a capture/compare register (including a shadow register), an input stage for capture (with a digital filter, multiplexing, and Prescaler) and an output stage (with comparator and output control). The output stage generates an intermediate waveform which is then used for reference: OCxRef (active high). The polarity acts at the end of the chain.
![image](https://github.com/vasanthkumarch/EXPERIMENT--07-SQUARE-WAVE-GENERATION-AT-THE-OUTPUT-PIN-USING-TIMER/assets/36288975/87457b57-4311-440b-8cbe-a9d78db4335a)

STM32 Timers In PWM Mode

Pulse width modulation mode allows generating a signal with a frequency determined by the value of the TIMx_ARR register and a duty cycle determined by the value of the TIMx_CCRx register. The PWM mode can be selected independently on each channel (one PWM per OCx output) by writing 110 (PWM mode 1) or ‘111 (PWM mode 2) in the OCxM bits in the TIMx_CCMRx register. The user must enable the corresponding preload register by setting the OCxPE bit in the TIMx_CCMRx register, and eventually the auto-reload preload register by setting the ARPE bit in the TIMx_CR1 register.

OCx polarity is software programmable using the CCxP bit in the TIMx_CCER register. It can be programmed as active high or active low. For applications where you need to generate complementary PWM signals, this option will be suitable for you.

In PWM mode (1 or 2), TIMx_CNT and TIMx_CCRx are always compared to determine whether TIMx_CCRx≤TIMx_CNT or TIMx_CNT≤TIMx_CCRx (depending on the direction of the counter).

The timer is able to generate PWM in edge-aligned mode or center-aligned mode depending on the CMS bits in the TIMx_CR1 register.
STM32 PWM Frequency

In various applications, you’ll be in need to generate a PWM signal with a specific frequency. In servo motor control, LED drivers, motor drivers, and many more situations where you’ll be in need to set your desired frequency for the output PWM signal.

The PWM period (1/FPWM) is defined by the following parameters: ARR value, the Prescaler value, and the internal clock itself which drives the timer module FCLK. The formula down below is to be used for calculating the FPWM for the output. You can set the clock you’re using, the Prescaler, and solve for the ARR value in order to control the FPWM and get what you want.

STM32 PWM Frequency Formula - STM32 PWM Frequency Equation
![image](https://github.com/vasanthkumarch/EXPERIMENT--07-SQUARE-WAVE-GENERATION-AT-THE-OUTPUT-PIN-USING-TIMER/assets/36288975/aca8a20e-9b99-40c1-bada-f31accaa2ae9)

STM32 PWM Duty Cycle

In normal settings, assuming you’re using the timer module in PWM mode and generating PWM signal in edge-aligned mode up-counting configuration. The duty cycle percentage is controlled by changing the value of the CCRx register. And the duty cycle equals (CCRx/ARR) [%].
![image](https://github.com/vasanthkumarch/EXPERIMENT--07-SQUARE-WAVE-GENERATION-AT-THE-OUTPUT-PIN-USING-TIMER/assets/36288975/58ce0807-331e-49f7-bc8d-373f82592a92)



## Procedure:
Step1: Open CubeMX & Create New Project
 ![image](https://user-images.githubusercontent.com/36288975/226189166-ac10578c-c059-40e7-8b80-9f84f64bf088.png)


Step2: Choose The Target MCU & Double-Click Its Name select the target to be programmed  as shown below and click on next 

 ![image](https://user-images.githubusercontent.com/36288975/226189215-2d13ebfb-507f-44fc-b772-02232e97c0e3.png)
![image](https://user-images.githubusercontent.com/36288975/226189230-bf2d90dd-9695-4aaf-b2a6-6d66454e81fc.png)

![image](https://user-images.githubusercontent.com/36288975/226189280-ed5dcf1d-dd8d-43ae-815d-491085f4863b.png)

Step3: Configure Timer2 Peripheral To Operate In PWM Mode With CH1 Output
![image](https://github.com/vasanthkumarch/EXPERIMENT--07-SQUARE-WAVE-GENERATION-AT-THE-OUTPUT-PIN-USING-TIMER/assets/36288975/682c851a-7dfe-4089-8395-f76088d43896)


Step4: Set The RCC External Clock Source
![image](https://github.com/vasanthkumarch/EXPERIMENT--07-SQUARE-WAVE-GENERATION-AT-THE-OUTPUT-PIN-USING-TIMER/assets/36288975/8888af3b-63e2-4760-a51b-17b477763941)


STM32 RCC External Clock Selection CubeMX

Step5: Go To The Clock Configuration

Step6: Set The System Clock To Be 72MHz
![image](https://github.com/vasanthkumarch/EXPERIMENT--07-SQUARE-WAVE-GENERATION-AT-THE-OUTPUT-PIN-USING-TIMER/assets/36288975/4ea03faa-fb90-4b31-8079-3db5f959f2c3)


Step7: Name & Generate The Project Initialization Code For CubeIDE or The IDE You’re Using



Step8.  Creating Proteus project and running the simulation
We are now at the last part of step by step guide on how to simulate STM32 project in Proteus.

Step9. Create a new Proteus project and place STM32F40xx i.e. the same MCU for which the project was created in STM32Cube IDE. 
14. After creation of the circuit as per requirement as shown below 

 ![image](https://github.com/vasanthkumarch/EXPERIMENT--07-SQUARE-WAVE-GENERATION-AT-THE-OUTPUT-PIN-USING-TIMER/assets/36288975/4f377f5e-bdda-489e-a416-c712c893831d)

Step10. Double click on the the MCU part to open settings. Next to the Program File option, give full path to the Hex file generated using STM32Cube IDE. Then set the external crystal frequency to 8M (i.e. 8 MHz). Click OK to save the changes.

 
Step14. click on debug and simulate using simulation as shown below 
 ![image](https://github.com/vasanthkumarch/EXPERIMENT--07-SQUARE-WAVE-GENERATION-AT-THE-OUTPUT-PIN-USING-TIMER/assets/36288975/b8efbfc2-f0c5-4106-8117-3a6e7ac87f6c)


 

  

## STM 32 CUBE PROGRAM :

```
#include "main.h"
#include "string.h"
#include "stdio.h"

/* Private includes ----------------------------------------------------------*/
/* USER CODE BEGIN Includes */

/* USER CODE END Includes */

/* Private typedef -----------------------------------------------------------*/
/* USER CODE BEGIN PTD */

/* USER CODE END PTD */

/* Private define ------------------------------------------------------------*/
/* USER CODE BEGIN PD */
/* USER CODE END PD */

/* Private macro -------------------------------------------------------------*/
/* USER CODE BEGIN PM */

/* USER CODE END PM */

/* Private variables ---------------------------------------------------------*/
ADC_HandleTypeDef hadc1;

UART_HandleTypeDef huart2;

/* USER CODE BEGIN PV */

/* USER CODE END PV */

/* Private function prototypes -----------------------------------------------*/
void SystemClock_Config(void);
static void MX_GPIO_Init(void);
static void MX_ADC1_Init(void);
static void MX_USART2_UART_Init(void);
/* USER CODE BEGIN PFP */

/* USER CODE END PFP */

/* Private user code ---------------------------------------------------------*/
/* USER CODE BEGIN 0 */

/* USER CODE END 0 */
uint16_t adcval;
char msg[20];
/**
  * @brief  The application entry point.
  * @retval int
  */
int main(void)
{
  /* USER CODE BEGIN 1 */

  /* USER CODE END 1 */

  /* MCU Configuration--------------------------------------------------------*/

  /* Reset of all peripherals, Initializes the Flash interface and the Systick. */
  HAL_Init();

  /* USER CODE BEGIN Init */

  /* USER CODE END Init */

  /* Configure the system clock */
  SystemClock_Config();

  /* USER CODE BEGIN SysInit */

  /* USER CODE END SysInit */

  /* Initialize all configured peripherals */
  MX_GPIO_Init();
  MX_ADC1_Init();
  MX_USART2_UART_Init();
  /* USER CODE BEGIN 2 */

  /* USER CODE END 2 */

  /* Infinite loop */
  /* USER CODE BEGIN WHILE */
  while (1)
  {
	      uint32_t adcval = 0;

	      HAL_ADC_Start(&hadc1);                      // 1. Start ADC

	      HAL_ADC_PollForConversion(&hadc1, 20);      // 2. Wait for conversion

	      adcval = HAL_ADC_GetValue(&hadc1);          // 3. Read ADC value

	      sprintf(msg, "ADC: %lu\r\n", adcval);       // Format data

	      HAL_UART_Transmit(&huart2, (uint8_t *)msg, strlen(msg), HAL_MAX_DELAY);

	      HAL_Delay(5000);
  }
  /* USER CODE END 3 */
}

/**
  * @brief System Clock Configuration
  * @retval None
  */
void SystemClock_Config(void)
{
  RCC_OscInitTypeDef RCC_OscInitStruct = {0};
  RCC_ClkInitTypeDef RCC_ClkInitStruct = {0};
  RCC_PeriphCLKInitTypeDef PeriphClkInit = {0};

  /** Configure the main internal regulator output voltage
  */
  HAL_PWREx_ControlVoltageScaling(PWR_REGULATOR_VOLTAGE_SCALE1);
  /** Initializes the RCC Oscillators according to the specified parameters
  * in the RCC_OscInitTypeDef structure.
  */
  RCC_OscInitStruct.OscillatorType = RCC_OSCILLATORTYPE_HSI;
  RCC_OscInitStruct.HSIState = RCC_HSI_ON;
  RCC_OscInitStruct.HSIDiv = RCC_HSI_DIV1;
  RCC_OscInitStruct.HSICalibrationValue = RCC_HSICALIBRATION_DEFAULT;
  RCC_OscInitStruct.PLL.PLLState = RCC_PLL_NONE;
  if (HAL_RCC_OscConfig(&RCC_OscInitStruct) != HAL_OK)
  {
    Error_Handler();
  }
  /** Initializes the CPU, AHB and APB buses clocks
  */
  RCC_ClkInitStruct.ClockType = RCC_CLOCKTYPE_HCLK|RCC_CLOCKTYPE_SYSCLK
                              |RCC_CLOCKTYPE_PCLK1;
  RCC_ClkInitStruct.SYSCLKSource = RCC_SYSCLKSOURCE_HSI;
  RCC_ClkInitStruct.AHBCLKDivider = RCC_SYSCLK_DIV1;
  RCC_ClkInitStruct.APB1CLKDivider = RCC_HCLK_DIV1;

  if (HAL_RCC_ClockConfig(&RCC_ClkInitStruct, FLASH_LATENCY_0) != HAL_OK)
  {
    Error_Handler();
  }
  /** Initializes the peripherals clocks
  */
  PeriphClkInit.PeriphClockSelection = RCC_PERIPHCLK_USART2|RCC_PERIPHCLK_ADC;
  PeriphClkInit.Usart2ClockSelection = RCC_USART2CLKSOURCE_PCLK1;
  PeriphClkInit.AdcClockSelection = RCC_ADCCLKSOURCE_SYSCLK;
  if (HAL_RCCEx_PeriphCLKConfig(&PeriphClkInit) != HAL_OK)
  {
    Error_Handler();
  }
}

/**
  * @brief ADC1 Initialization Function
  * @param None
  * @retval None
  */
static void MX_ADC1_Init(void)
{

  /* USER CODE BEGIN ADC1_Init 0 */

  /* USER CODE END ADC1_Init 0 */

  ADC_ChannelConfTypeDef sConfig = {0};

  /* USER CODE BEGIN ADC1_Init 1 */

  /* USER CODE END ADC1_Init 1 */
  /** Configure the global features of the ADC (Clock, Resolution, Data Alignment and number of conversion)
  */
  hadc1.Instance = ADC1;
  hadc1.Init.ClockPrescaler = ADC_CLOCK_SYNC_PCLK_DIV2;
  hadc1.Init.Resolution = ADC_RESOLUTION_12B;
  hadc1.Init.DataAlign = ADC_DATAALIGN_RIGHT;
  hadc1.Init.ScanConvMode = ADC_SCAN_DISABLE;
  hadc1.Init.EOCSelection = ADC_EOC_SINGLE_CONV;
  hadc1.Init.LowPowerAutoWait = DISABLE;
  hadc1.Init.LowPowerAutoPowerOff = DISABLE;
  hadc1.Init.ContinuousConvMode = ENABLE;
  hadc1.Init.NbrOfConversion = 1;
  hadc1.Init.DiscontinuousConvMode = DISABLE;
  hadc1.Init.ExternalTrigConv = ADC_SOFTWARE_START;
  hadc1.Init.ExternalTrigConvEdge = ADC_EXTERNALTRIGCONVEDGE_NONE;
  hadc1.Init.DMAContinuousRequests = DISABLE;
  hadc1.Init.Overrun = ADC_OVR_DATA_PRESERVED;
  hadc1.Init.SamplingTimeCommon1 = ADC_SAMPLETIME_1CYCLE_5;
  hadc1.Init.SamplingTimeCommon2 = ADC_SAMPLETIME_1CYCLE_5;
  hadc1.Init.OversamplingMode = DISABLE;
  hadc1.Init.TriggerFrequencyMode = ADC_TRIGGER_FREQ_HIGH;
  if (HAL_ADC_Init(&hadc1) != HAL_OK)
  {
    Error_Handler();
  }
  /** Configure Regular Channel
  */
  sConfig.Channel = ADC_CHANNEL_0;
  sConfig.Rank = ADC_REGULAR_RANK_1;
  sConfig.SamplingTime = ADC_SAMPLINGTIME_COMMON_1;
  if (HAL_ADC_ConfigChannel(&hadc1, &sConfig) != HAL_OK)
  {
    Error_Handler();
  }
  /* USER CODE BEGIN ADC1_Init 2 */

  /* USER CODE END ADC1_Init 2 */

}

/**
  * @brief USART2 Initialization Function
  * @param None
  * @retval None
  */
static void MX_USART2_UART_Init(void)
{

  /* USER CODE BEGIN USART2_Init 0 */

  /* USER CODE END USART2_Init 0 */

  /* USER CODE BEGIN USART2_Init 1 */

  /* USER CODE END USART2_Init 1 */
  huart2.Instance = USART2;
  huart2.Init.BaudRate = 115200;
  huart2.Init.WordLength = UART_WORDLENGTH_8B;
  huart2.Init.StopBits = UART_STOPBITS_1;
  huart2.Init.Parity = UART_PARITY_NONE;
  huart2.Init.Mode = UART_MODE_TX_RX;
  huart2.Init.HwFlowCtl = UART_HWCONTROL_NONE;
  huart2.Init.OverSampling = UART_OVERSAMPLING_16;
  huart2.Init.OneBitSampling = UART_ONE_BIT_SAMPLE_DISABLE;
  huart2.Init.ClockPrescaler = UART_PRESCALER_DIV1;
  huart2.AdvancedInit.AdvFeatureInit = UART_ADVFEATURE_NO_INIT;
  if (HAL_UART_Init(&huart2) != HAL_OK)
  {
    Error_Handler();
  }
  if (HAL_UARTEx_SetTxFifoThreshold(&huart2, UART_TXFIFO_THRESHOLD_1_8) != HAL_OK)
  {
    Error_Handler();
  }
  if (HAL_UARTEx_SetRxFifoThreshold(&huart2, UART_RXFIFO_THRESHOLD_1_8) != HAL_OK)
  {
    Error_Handler();
  }
  if (HAL_UARTEx_DisableFifoMode(&huart2) != HAL_OK)
  {
    Error_Handler();
  }
  /* USER CODE BEGIN USART2_Init 2 */

  /* USER CODE END USART2_Init 2 */

}

/**
  * @brief GPIO Initialization Function
  * @param None
  * @retval None
  */
static void MX_GPIO_Init(void)
{

  /* GPIO Ports Clock Enable */
  __HAL_RCC_GPIOA_CLK_ENABLE();

}

/* USER CODE BEGIN 4 */

/* USER CODE END 4 */

/**
  * @brief  This function is executed in case of error occurrence.
  * @retval None
  */
void Error_Handler(void)
{
  /* USER CODE BEGIN Error_Handler_Debug */
  /* User can add his own implementation to report the HAL error return state */
  __disable_irq();
  while (1)
  {
  }
  /* USER CODE END Error_Handler_Debug */
}

#ifdef  USE_FULL_ASSERT
/**
  * @brief  Reports the name of the source file and the source line number
  *         where the assert_param error has occurred.
  * @param  file: pointer to the source file name
  * @param  line: assert_param error line source number
  * @retval None
  */
void assert_failed(uint8_t *file, uint32_t line)
{
  /* USER CODE BEGIN 6 */
  /* User can add his own implementation to report the file name and line number,
     ex: printf("Wrong parameters value: file %s on line %d\r\n", file, line) */
  /* USER CODE END 6 */
}
#endif /* USE_FULL_ASSERT */

/************************ (C) COPYRIGHT STMicroelectronics ****END OF FILE*/
```



## Output screen shots of proteus  :
 <img width="1159" height="768" alt="Screenshot 2025-10-30 143318" src="https://github.com/user-attachments/assets/d56eab78-49fa-4c93-a6ca-e1762d92a567" />

 <img width="1376" height="874" alt="image" src="https://github.com/user-attachments/assets/935d235a-f940-4964-95e3-aba7672b2ac2" />
<img width="1376" height="875" alt="image" src="https://github.com/user-attachments/assets/8e39a883-4359-43ca-8403-a6ab27984128" />
<img width="1378" height="874" alt="image" src="https://github.com/user-attachments/assets/f4f5bcde-8c27-4182-85f8-da58740285c2" />


 ## CIRCUIT DIAGRAM (EXPORT THE GRAPHICS TO PDF AND ADD THE SCREEN SHOT HERE): 
 <img width="1038" height="730" alt="Screenshot 2025-10-30 143717" src="https://github.com/user-attachments/assets/aeb42747-df48-402f-a8e4-ff8d9276e97f" />


## DUTY CYCLE AND FREQUENCY CALCULATION 
FOR PULSE AT 50%

Amp = 5 * 1V = 5V

TON = 2.5 * 0.5 = 1.25ms

TOFF = 2.5 * 0.5 = 1.25ms

TOTAL TIME = 5 * 0.5 = 2.5ms

FREQUENCY = 1/(TOTAL TIME) = 0.4KHz

FOR PULSE AT 25%

Amp = 5 * 1V = 5V

TON = 1.25 * 0.5 = 0.625ms

TOFF= 3.75 * 0.5 = 1.875ms

TOTAL TIME = 2.5ms

FREQUENCY = 1/(TOTAL TIME) = 0.4KHz

FOR PULSE AT 75%

Amp = 5 * 1V = 5V

TON = 3.75 * 0.5 = 1.875ms

TOFF= 1.25 * 0.5 = 0.625ms

TOTAL TIME = 2.5ms

FREQUENCY = 1/(TOTAL TIME) = 0.4KHz



## Result :
A PWM Signal is generated using the following frequency and various duty cycles are simulated 




