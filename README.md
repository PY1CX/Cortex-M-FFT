# Cortex-M-FFT
Testing the FFT performance of Cortex-M microcontrollers on ST Nucleo boards

Results for arm_cfft_f32 function:

Core | 32 points | 512 points | 1024 points | Performace gain in % | 
:---: | :---: | :---: | :---: | :---: |
Cortex-M0 | 637 | 21 | 9 | 0% | 
Cortex-M3 | 2215 | 72 | 31 | 345% |
Cortex-M4 | 133460 | 7113 | 2924 | 8445%
Cortex-M7 With Cache Disabled | 160485 | 8038 | 3108 | 113% |
Cortex-M7 With Cache Enabled | 490595 | 24145 | 9807 | 307% |

Yes, the difference between non-FPU and FPU-present cores blew my mind when I saw the results. 

## How to enable the cache on STM32H7 MCU:

Just enable the cache with the following code, before the function HAL_Init();

```
/* Enable I-Cache */
SCB_EnableICache();

/* Enable D-Cache */
SCB_EnableDCache();
```

## How to link CMSIS-PACK (CMSIS-DSP) with projects generated from STM32CubeMX in Atollic TrueStudio.

With Atollic TrueStudio open:
File -> C Project -> CMSIS C/C++ Project -> Atollic ARM Tools (use a mock-up name for this project).
Next
Next
Select your microcontroller from the STMicroelectronics tab.
Next
Finish

With both projects open on your Atollic TrueStudio IDE, from the mock-up project you copy the following files to your STM32CubeMX project:
RTE folder
(projectname).rteconfig 

On your real project to to the Properties (Project -> Properties)

C/C++ Build -> Settings 

C Compiler -> Symbos add:

ARM_MATH_CM(your CM processor)
_FPU_PRESENT= (0 or 1 depending on the microcontroller your're using)

C Linker - Libraries

Libraries ( Where you can see all pre-compiled libraries https://github.com/ARM-software/CMSIS/tree/master/CMSIS/Lib/GCC )

For M3 for example, add:

:libarm_cortexM3l_math.a

C Linker - Library Search Path:

Add: "${cmsis_pack_root}/ARM/CMSIS/5.3.0/CMSIS/Lib/GCC"

Remember, you NEED to install CMSIS Packs on Atollic! A tip to see if everything went smooth: Ctrl+Click the arm_math.h include line, if you done everything right you should open the file.      
