This is a remake of something I did in the early two-thousands to learn how heap and stack exploit development worked. DEP, ASLR, heap and stack cookies, and shadow stacks now exist and I'm doing it to learn mitigation bypasses across platforms. Windows 10, Debian(5.15+), and macOS Monterey will be the platforms used. The goal is only to get code execution not to break out of sandboxes or get root. I may later do better shellcode.</br>
# Payloads
MSVC: HTTP reverse shell</br>
GCC: HTTP reverse shell</br>
Xcode: HTTP reverse shell</br>
</br>
# MSVC</br>
* stack</br>
* stack HW /NXCOMPAT + /DYNAMICBASE</br>
* stack HW /NXCOMPAT + /DYNAMICBASE</br>
* stack HW /NXCOMPAT + /DYNAMICBASE + CET/CET_SS/guard:cf</br>
* heap (W10 allocator hardening)</br>
* heap (W10 allocator hardening) + HW /NXCOMPAT + /DYNAMICBASE</br>
* heap (W10 allocator hardening) + HW /NXCOMPAT + /DYNAMICBASE</br>
* heap (W10 allocator hardening) + HW /NXCOMPAT + /DYNAMICBASE+ CET/CET_SS/guard:cf</br>

</br></br>
# GCC</br>
* stack</br>
* stack -fstack-protector-all + -fstack-clash-protection + -Wl,nxcompat</br>
* stack -fstack-protector-all + -fstack-clash-protection + -Wl,nxcompat + -fpie</br>
* stack -fstack-protector-all + -fstack-clash-protection + -Wl,nxcompat + -fpie + CET/CET_SS/-fcf-protection=full</br>
* heap (allocator hardening)</br>
* heap (allocator hardening) + -fstack-protector-all + -fstack-clash-protection</br>
* heap (allocator hardening) + -fstack-protector-all + -fstack-clash-protection + -Wl,nxcompat + -fpie</br>
* heap (allocator hardening) + -fstack-protector-all + -fstack-clash-protection + -Wl,nxcompat + -fpie + CET/CET_SS/-fcf-protection=full</br>

</br></br>
# Xcode</br>
* TODO(should be on par with GCC since they don't port ARM tech to x86</br>
* NOTE: Gatekeeper and Xprotect have no stack or heap mitigations but may have HIPS or HIDS that detect exceptions or shellcode</br>
</br>
