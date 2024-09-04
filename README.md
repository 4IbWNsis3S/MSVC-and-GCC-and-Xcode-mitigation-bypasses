This is a remake of something I did in the early two-thousands to learn how heap and stack exploit development worked. DEP, ASLR, heap cookies, and shadow stack now exists. I'm doing it to learn mitigation bypasses across platforms. Windows 11(x86-64), Debian(12.5+)(x86-64), and macOS 14(ARMv8.6) will be the platforms used; helping others along the way with what is an obscure field of software engineering and IT security that has only primitive outdated references on search engines.<br/><br/>The goal is only to get code execution and do a reverse shell, and not to break out of sandboxes or get root.</br>
# Payloads
MSVC: HTTP reverse shell</br>
GCC: HTTP reverse shell</br>
Xcode: HTTP reverse shell</br>
</br>
# MSVC(SDK 10.0+, VS 142+)</br>
* stack</br>
* stack HW /NXCOMPAT + /DYNAMICBASE + /HYENTROPYVA + /GS</br>
* stack HW /NXCOMPAT + /DYNAMICBASE + /HYENTROPYVA + /GS + /CETCOMPAT + /guard:cf</br>
* heap (W11 allocator hardening)</br>
* heap (W11 allocator hardening) + HW /NXCOMPAT + /DYNAMICBASE + /HYENTROPYVA + /GS</br>
* heap (W11 allocator hardening) + HW /NXCOMPAT + /DYNAMICBASE + /HYENTROPYVA + /GS + /CETCOMPAT + /guard:cf</br>

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
* TODO</br>
* NOTE: Gatekeeper and Xprotect have no stack or heap mitigations but may have HIPS or HIDS that detect exception chains or shellcode; on top of what the compiler implements..</br>
* This will probably come last in a lot of cases because I don't *yet* have modern Apple hardware with features that support things like MTE(because it's ARM) and DEP(I haven't bought apple since they dropped PPC in 2005(M9970 owner)). I'm planning on getting something with a M3 Max for this(so I can use it for video transcoding and editing later(economics and stuff))
</br></br></br>
# NOTES
* This project will probably finish over time since I do it in my free time and people who understand what is going on likely won't pick up some of the workload
* This will not teach how to find exploitable memory bugs. That is commonly done with experienced static analysis and fuzzing. Some types of bugs can't be seen by any experienced eye in static analysis, and that along with the the tooling for format and protocol fuzzing is why there aren't many zero-day level security people. Finding bugs in a large code base is a lot harder than learning shellcode development and debugging. In 2021 it's so hard that "black box" fuzzing is basically never used like it was prior to DEP and W^X
* I don't bother with W^X. If I can bypass HW DEP/NX I can bypass W^X
* This isn't vaporware. I already have non-mitigation examples done. I just need to document shellcode dev flow, and modify ROP payloads with working mitigation bypasses. CET/CET_SS is bleeding-edge mitigation and currently only unreliable race-condition-pointer and semi-stable COOP methods are known
