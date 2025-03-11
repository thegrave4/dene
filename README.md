#!/usr/bin/env python3
import subprocess
import time
import os

def get_connected_devices():
    # bluetoothctl info komutu, bağlı cihaz bilgilerini getirir.
    result = subprocess.run(["bluetoothctl", "info"], capture_output=True, text=True)
    return result.stdout

def start_wifi_setup():
    # WiFi ayar arayüzünü başlat (wifi_setup.py dosyasını arka planda çalıştırır)
    subprocess.Popen(["/usr/bin/python3", "/usr/local/bin/wifi_setup.py"])
    print("WiFi ayar arayüzü başlatıldı.")

if __name__ == "__main__":
    print("Bluetooth bağlantıları dinleniyor...")
    while True:
        devices_info = get_connected_devices()
        # 'Device' ifadesi varsa, bağlantı olmuş demektir
        if "Device" in devices_info:
            print("Bluetooth ile bağlantı tespit edildi!")
            start_wifi_setup()
            # İsteğe bağlı: Bağlantı tespit edildikten sonra döngüyü bitirir veya belirli aralıklarla kontrol etmeye devam edebilirsiniz.
            break
        time.sleep(5)
