# dingJMax

The given binary is an AMD64 ELF file. A flag is shown on the screen, and its value is changed when the user presses a key. The changes depend on a current time counter inside the application. In order to get the correct flag, we need to hit all the notes at the perfect time (which seems to be impossible for me to do manually). So I patched the binary to automatically trigger flag transformations on the right condition. Note that the program's logic recalculates internal state after recording a key press, so we need to perform byte check on the previous DWORD.

The patched binary is attached inside this folder.

The flag is `SCTF{I_w0u1d_l1k3_70_d3v3l0p_GUI_v3rs10n_n3x7_t1m3}`.