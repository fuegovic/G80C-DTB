# 🎮 Fuegovic’s R36S Clone Analog Stick Fix  

**Board**: G80C-MB V1.1

**OS**: [AeolusUX/ArkOS-K36](https://github.com/AeolusUX/ArkOS-K36)  

**Goal**: Fix analog stick mapping issues on R36S clones.  

---

## 🔧 Fixes  

- **Right analog stick flipped 180°** (on newer kernels)  
- **Left + Right X-axis crossover** (on older kernels)  
- Both issues resolved with the patched files included in this repo.  

---

## ⚠️ Known Issues  

- **Headphones**: audio flickers between headphone out and onboard speaker when headphones are connected.  

---

## 📦 What’s Included  

- ✅ `image` (working kernel image)  
- ✅ `rk3326-g80c.dtb` (patched device tree blob)  
- ✅ `extlinux/` folder (preconfigured)  
- ✅ `rk3326-g80c.dts` (patched device tree source, for reference/editing)  

---

## 🚀 Installation  

1. Mount the **boot partition** of your SD card.  
2. Copy these files from the repo into the **boot partition**:  
   - `image`  
   - `rk3326-g80c.dtb`  
   - `extlinux/` (folder)  
3. Safely unmount and reboot your device.  

---

## 🛠️ DTS Patch (for reference only)  

If you want to apply the fix manually instead of using the provided DTS/DTB, in the `play_joystick` node of your DTS swap the `linux,code` values for the X-axis channels:

```dts
left-x {
    label = "left x";
    adc-chan = <0x00>;
    linux,code = <0x03>;  // was 0x00
    press-threshold-microvolt = <0x6d6>;
};

right-x {
    label = "right x";
    adc-chan = <0x02>;
    linux,code = <0x00>;  // was 0x03
    press-threshold-microvolt = <0x6d6>;
};
````

Recompile with:

```bash
dtc -I dts -O dtb -o rk3326-g80c.dtb rk3326-g80c.dts
```

---

## 📚 Sources

* Base DTS/DTB files: [Vi-K36 EE-Clones-DTB repo](https://github.com/Vi-K36/EE-Clones-DTB/tree/main/R36S%20EE-Clone/ArkOS%20%28P5%29%20%5BG80C%20board%5D%20%28shared%20by%20ptv%29)
* ArkOS-K36: [AeolusUX/ArkOS-K36](https://github.com/AeolusUX/ArkOS-K36)


Do you want me to also add a **“File tree preview”** section (like `boot/` → files) so users know exactly how the repo contents map to their SD card’s boot partition?
```
