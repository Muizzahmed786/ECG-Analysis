# WFDB Record Object Keys

When you read an ECG file using `wfdb.rdrecord()`, it returns a `Record` object that contains both the ECG signal and its metadata. 

| Key | Description |
|------|-------------------|
| `record_name` | Name of the ECG record (without `.hea` or `.dat`). |
| `n_sig` | Number of ECG leads (signals) in the record (e.g., 9 or 12). |
| `fs` | Sampling frequency (samples recorded per second). For this dataset, it is **500 Hz**. |
| `counter_freq` | Internal timing frequency used by the recording device (rarely needed). |
| `base_counter` | Starting value of the device's internal counter (usually ignored). |
| `sig_len` | Total number of samples recorded for each lead. |
| `base_time` | Time when the ECG recording started (if available). |
| `base_date` | Date when the ECG recording was taken (if available). |
| `comments` | Extra information or notes stored in the header file. |
| `sig_name` | Names of all ECG leads (e.g., `I`, `II`, `III`, `V1`, etc.). |
| `p_signal` | **The actual ECG signal values in physical units (mV).** This is the main data you'll analyze. |
| `d_signal` | Raw digital signal values before converting them to mV. Usually not needed. |
| `e_p_signal` | Expanded physical signal (used for special multi-sample formats). Rarely used. |
| `e_d_signal` | Expanded digital signal. Rarely used. |
| `file_name` | Name of the `.dat` file(s) storing the ECG signal. |
| `fmt` | Storage format used inside the `.dat` file. Mainly useful for low-level file handling. |
| `samps_per_frame` | Number of samples stored in each frame. Usually `1` for standard ECGs. |
| `skew` | Time offset between different leads, if any. Usually `0`. |
| `byte_offset` | Starting position inside the `.dat` file where signal data begins. |
| `adc_gain` | Conversion factor from digital values to millivolts (mV). |
| `baseline` | Baseline digital value corresponding to **0 mV**. |
| `units` | Measurement unit of the signal (usually `mV`). |
| `adc_res` | Resolution of the Analog-to-Digital Converter (ADC), in bits. |
| `adc_zero` | Digital value representing zero voltage. |
| `init_value` | First sample value for each lead. |
| `checksum` | Value used to verify that the ECG file is not corrupted. |
| `block_size` | Storage block size in the `.dat` file. Usually not needed for analysis. |

---

## Keys you'll use most in this project

These are the ones you'll work with almost all the time:

- `record.fs` → Sampling frequency
- `record.sig_name` → ECG lead names
- `record.n_sig` → Number of leads
- `record.sig_len` → Number of samples
- `record.p_signal` → ECG waveform data (**most important**)
- `record.units` → Signal units (mV)

Everything else is mostly metadata or information required internally by the WFDB library.