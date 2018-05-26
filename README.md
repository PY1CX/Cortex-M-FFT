# Cortex-M-FFT
Testing the FFT performance of Cortex-M microcontrollers on ST Nucleo boards


How to link CMSIS-PACK (CMSIS-DSP) with projects generated from STM32CubeMX in Atollic TrueStudio.

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

Remember, you NEED to install CMSIS Packs on Atollic!
