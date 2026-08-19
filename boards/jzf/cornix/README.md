# Cornix Choc v1 

- Module: ebyte E73-2G4M08S1C (link)[https://www.cdebyte.com/products/E73-2G4M08S1C]
- Soc: nrf52840
- Project name: SP46

version: stock v1 choc

## Firmware changes

This fork keeps the stock Cornix hardware definition and adds the following
firmware behavior:

- NKRO is enabled for USB and Bluetooth HID with
  `CONFIG_ZMK_HID_REPORT_TYPE_NKRO=y` and
  `CONFIG_ZMK_HID_KEYBOARD_NKRO_EXTENDED_REPORT=y` in `config/cornix.conf`.
  This allows the keyboard to report more simultaneous key presses than the
  standard six-key boot keyboard report, subject to host support.
- The active layers are ordered `BASE`, `NUM`, `FN`, and `PLOVER`. The former
  ALT layout is now BASE. NUM and FN are momentary layers from BASE.
- Double-tapping the BASE/PLOVER layer key within 250 ms switches layers and
  sends the PHROLG steno chord (`E + R + F + V + O + L`) simultaneously. The
  default Plover command dictionary maps PHROLG to `{PLOVER:TOGGLE}`. Plover
  must already be running; ZMK only sends the chord and does not launch the
  application. The PLOVER layer is intentionally left open for later mapping.
- FN Bluetooth profile keys select profiles 0, 1, and 2 on tap. Holding one
  for 600 ms selects that profile and clears its bond, providing a recovery
  path when a host's saved Bluetooth keys no longer match the keyboard.
- The second rotary encoder sends mouse-wheel events. The right-half build
  includes pointing support so those events reach the central half.

After clearing a Bluetooth bond, forget the Cornix on the host before pairing
again. Reflashing firmware alone does not erase stored Bluetooth bonds.

## PCB layout

- physical-layout:  https://zmk-physical-layout-converter.streamlit.app/?layout=H4sIAAAAAAACA-2VTUvEMBCG7_srQs9rSWaatvHmXfCiBxER74KwrmAp-99NP7aZlmnGHIUUStOZt28neUKmPyhVfLx3n9_nr-JW9f7VB-7vnh-eHt-sXkKLykde5ohSvSp-fECX-qiKbhxZvbqMuhy3cpMmByIHywiQCDSTryQDm1ZQW9oUuSNyXMt1xS2PJh9w8zGGOm4sG-4DSKvYYJo-8PeVRYHzeSB5gbARCBuJMF9BQMrnHcljnJmRmHkHcPRq48h21hQFQYDireJUdgRABAIWELCAhGWnhFr4Q7MsAp9vSd7GwYIEFiSw3gHjKPdIoKQIMFGCiRJMZCcaSsCyRhZmEDR-dJom73AYB5inbtQ2PG7yj_W5Us2OMO2pPxo2ZV2tDqfZ3pbYbuOD-02avSNr1tirx2rSzm9swcVQeOzSkj3k4QjHAYp7aFLMgtfxOeuvjb2C3NhzY8-NPTf23NhzY8-N_R839sNwX34BxrzaZccPAAA%3D
