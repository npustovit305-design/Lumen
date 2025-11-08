# LuminaOS (Debian 12, GNOME, Calamares)

LuminaOS — пользовательский дистрибутив на базе Debian 12 (bookworm) с окружением GNOME, классическими обновлениями APT, установкой через Calamares и полнодисковым шифрованием LUKS (LVM, btrfs).

## Стек
- База: Debian 12 (amd64)
- DE: GNOME (светлая тема по умолчанию)
- Установщик: Calamares (GUI)
- Шифрование: LUKS + LVM, btrfs (@, @home), swapfile
- Обновления: APT (main, contrib, non-free, non-free-firmware)

## Структура
- branding/luminaos/ — логотипы (SVG), ассеты бренда
- live-build/ — конфигурация сборки live ISO (Debian live-build)
- calamares/branding/luminaos/ — брендирование Calamares
- calamares/modules/ — модули Calamares (разметка, пользователи, локаль)
- docs/ — документация (WSL2/CI)

## Быстрая сборка (WSL2 Ubuntu)
1) Включите WSL2 и установите Ubuntu из Microsoft Store.
2) В WSL2:
```
sudo apt update
sudo apt install -y live-build debootstrap syslinux-common isolinux \
  squashfs-tools xorriso git wget curl ca-certificates \
  calamares calamares-settings-debian \
  cryptsetup lvm2 btrfs-progs \
  task-gnome-desktop gdm3 network-manager \
  pipewire wireplumber fwupd cups \
  firmware-misc-nonfree mesa-vulkan-drivers intel-media-driver \
  ffmpeg gstreamer1.0-plugins-base gstreamer1.0-plugins-good \
  gstreamer1.0-plugins-bad gstreamer1.0-libav
```
3) Настройте live-build (уже предсконфигурирован через auto/config):
```
cd live-build
sudo lb clean
sudo ./auto/config
sudo lb build
```
Артефакт: `live-image-amd64.hybrid.iso` в корне проекта.

## Примечания
- Plymouth/GRUB ассеты будут добавлены на следующих шагах (требуются PNG для Plymouth). Сейчас бренд применяется в Calamares и GNOME обоях.
- Для новых Intel iGPU можно собирать ISO с ядром из backports (добавим профиль позднее).

