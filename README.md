This is a remake of something I did in the early two-thousands to learn how heap and stack exploit development worked. DEP, ASLR, heap and stack cookies, and shadow stacks now exist and I'm doing it to learn mitigation bypasses across platforms. Windows 10, Debian(5.15+), and macOS Monterey will be the platforms used; helping others along the way with what is an obscure field of software engineering and IT security that has only primitive out-dated references on search engines. The goal is only to get code execution not to break out of sandboxes or get root. I may later do better shellcode that isn't just HTTP polling for commands.</br>
# Payloads
MSVC: HTTP reverse shell</br>
GCC: HTTP reverse shell</br>
Xcode: HTTP reverse shell</br>
</br>
# MSVC(SDK 10.0+, VS 142+)</br>
* stack</br>
* stack HW /NXCOMPAT + /DYNAMICBASE</br>
* stack HW /NXCOMPAT + /DYNAMICBASE</br>
* stack HW /NXCOMPAT + /DYNAMICBASE + CET/CET_SS/guard:cf</br>
* heap (W10 allocator hardening)</br>
* heap (W10 allocator hardening) + HW /NXCOMPAT + /DYNAMICBASE</br>
* heap (W10 allocator hardening) + HW /NXCOMPAT + /DYNAMICBASE</br>
* heap (W10 allocator hardening) + HW /NXCOMPAT + /DYNAMICBASE+ CET/CET_SS/guard:cf</br>

</br></br>
# GCC(11.2+)</br>
* stack</br>
* stack -fstack-protector-all + -fstack-clash-protection + -Wl,nxcompat HW</br>
* stack -fstack-protector-all + -fstack-clash-protection + -Wl,nxcompat HW + -fpie</br>
* stack -fstack-protector-all + -fstack-clash-protection + -Wl,nxcompat HW+ -fpie + CET/CET_SS/-fcf-protection=full</br>
* heap (allocator hardening)</br>
* heap (allocator hardening) + -fstack-protector-all + -fstack-clash-protection</br>
* heap (allocator hardening) + -fstack-protector-all + -fstack-clash-protection + -Wl,nxcompat HW + -fpie</br>
* heap (allocator hardening) + -fstack-protector-all + -fstack-clash-protection + -Wl,nxcompat HW + -fpie + CET/CET_SS/-fcf-protection=full</br>

</br></br>
# Xcode</br>
* TODO(should be on par with GCC since they don't port ARM tech to x86)</br>
* NOTE: Gatekeeper and Xprotect have no stack or heap mitigations but may have HIPS or HIDS that detect exceptions or shellcode</br>
* This will probably come last in a lot of cases because I don't *yet* have modern Apple hardware with features that support things like CET and DEP(My apple stuff is still PPC)
</br></br></br>
# NOTES
* This project will probably finish over time since I do it in my free time and people who understand what is going on likely won't pick up some of the workload
* This will not teach how to find exploitable memory bugs. That is commonly done with experienced static analysis and fuzzing. Some types of bugs can't be seen by any experienced eye in static analysis, and that along with the the tooling for format and protocol fuzzing is why there aren't many zero-day level security people. Finding bugs in a large code base is a lot harder than learning shellcode development and debugging. In 2021 it's so hard that "black box" fuzzing is basically never used like it was prior to DEP and W^X
* I don't bother with W^X. If I can bypass HW DEP/NX I can bypass W^X
* This isn't vaporware. I already have non-mitigation examples done. I just need to document shellcode dev flow, and modify ROP payloads with working mitigation bypasses. CET/CET_SS is bleeding-edge mitigation and currently only race-condition-pointer methods are known
