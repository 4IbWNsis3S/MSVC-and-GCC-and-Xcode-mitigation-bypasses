MSVC: calc.exe dynamic paypload
GCC: reverse UDP shell
Xcode: Reverse UDP shell

MSVC{
stack
stack HW DEP + ASLR
stack HW DEP + ASLR + GS
stack HW DEP + ASLR + GS + CET/CET_SS
heap W10 heap-mitigations
heap W10 HW DEP + ASLR
heap W10 HW DEP + ASLR + GS
heap W10 HW DEP + ASLR + GS + CET/CET_SS
}

GCC{
stack
stack -fstack-protector-all + -fstack-clash-protection + -Wl,nxcompat
stack -fstack-protector-all + -fstack-clash-protection + -Wl,nxcompat + -fpie
stack -fstack-protector-all + -fstack-clash-protection + -Wl,nxcompat + -fpie + CET/CET_SS/-fcf-protection=full
heap
heap -fstack-protector-all + -fstack-clash-protection
heap -fstack-protector-all + -fstack-clash-protection + -Wl,nxcompat + -fpie
heap -fstack-protector-all + -fstack-clash-protection + -Wl,nxcompat + -fpie + CET/CET_SS/-fcf-protection=full
}

Xcode{
}
