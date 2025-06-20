# Dental Appointment Booking Script

## Overview

This Node.js script uses Puppeteer to automate the booking of dental appointments on the DentalHub website (specifically for Kilmarnock Smile Studio). It navigates through the appointment booking process, including selecting patient type, insurance, appointment type, provider, and time slots, and fills out patient information with validation. The script handles dynamic web elements, retries failed actions, and includes robust error handling.

## Features

- **Interactive CLI**: Prompts the user for patient details (e.g., name, date of birth, sex, mobile number, email, etc.).
- **Dynamic Navigation**: Extracts and displays available appointment types, providers, and time slots for user selection.
- **Robust Field Input**: Handles text and date fields with retries and validation to ensure accurate data entry.
- **Error Handling**: Retries failed selector searches, logs errors, and captures screenshots on failure.
- **Customizable**: Supports new/existing patient types, private/NHS insurance, and optional fields like medical considerations and callback preferences.
- **OTP Verification**: Prompts for and inputs a 4-digit OTP for booking confirmation.

## Prerequisites

- **Node.js**: Version 14 or higher.
- **Puppeteer**: For browser automation.
- **prompt-sync**: For synchronous user input in the CLI.
- **Brave Browser**: The script is configured to use Brave Browser (modify `executablePath` in the script if using a different browser like Chrome).

## Installation

1. Clone the repository:
   ```bash
   git clone https://github.com/your-username/dental-appointment-booking.git
   cd dental-appointment-booking
   ```

2. Install dependencies:
   ```bash
   npm install puppeteer prompt-sync
   ```

3. Ensure Brave Browser is installed and update the `executablePath` in the script if necessary. For example:
   - Linux: `/usr/bin/brave-browser`
   - Windows: `C:\\Program Files\\BraveSoftware\\Brave-Browser\\Application\\brave.exe`
   - macOS: `/Applications/Brave Browser.app/Contents/MacOS/Brave Browser`

## Usage

1. Run the script:
   ```bash
   node index.js
   ```

2. Follow the CLI prompts to input:
   - First and last name
   - Date of birth (DD/MM/YYYY)
   - Sex (Male/Female/Other)
   - Mobile number (e.g., +14155550132)
   - Email address
   - Appointment confirmation call preference (yes/no)
   - Medical considerations (optional)
   - Patient type (NewPatient/ExistingPatient)
   - Insurance type (Private/NHS)
   - Appointment type (from a list of available options)
   - Provider (from a list of available options)
   - Time slot (from available slots or browse previous/next weeks)
   - OTP code (received via SMS for verification)

3. The script will:
   - Navigate to the DentalHub booking page.
   - Accept cookies if prompted.
   - Fill in all required fields.
   - Display available appointment types, providers, and slots.
   - Allow slot preview and confirmation.
   - Handle OTP verification and complete the booking process.
   - Output the booking confirmation URL or save an error screenshot (`error-screenshot.png`) if something fails.

## Configuration

- **Browser Settings**: The script runs in non-headless mode (`headless: false`) for visibility. Set `headless: true` in the `puppeteer.launch` options for headless execution.
- **Timeouts and Retries**: Adjust `waitForSelectorWithRetry` retries and timeouts or `delay` times in the script for different network conditions.
- **Executable Path**: Update the `executablePath` in the script to match your browser’s installation path.

## Error Handling

- The script retries failed selector searches up to 3 times with a 2-second delay between attempts.
- If an error occurs, it logs the error and saves a screenshot (`error-screenshot.png`) for debugging.
- The browser is closed gracefully in the `finally` block to prevent resource leaks.

## Limitations

- **Website Dependency**: The script is tailored for the DentalHub website (specifically `https://uk.dentalhub.online`). Changes to the website’s structure or selectors may break the script.
- **Browser Dependency**: Configured for Brave Browser; other browsers may require path adjustments.
- **Network Reliability**: Slow or unstable connections may cause timeouts, which can be mitigated by adjusting timeout values.
- **OTP Dependency**: Requires manual input of the OTP received via SMS.

## Troubleshooting

- **Selector Not Found**: If a selector fails, check the website for updated DOM structure and update the corresponding selectors in the script.
- **Browser Not Found**: Ensure the `executablePath` points to the correct browser executable.
- **Timeout Errors**: Increase timeout values in `waitForSelectorWithRetry` or `page.goto`.
- **OTP Issues**: Verify the mobile number is correct and can receive SMS.

## Contributing

Contributions are welcome! Please submit a pull request or open an issue for bugs, improvements, or new features.

## License

This project is licensed under the MIT License. See the [LICENSE](LICENSE) file for details.

## Disclaimer

This script is for educational purposes only. Ensure compliance with the website’s terms of service and applicable laws when using automation tools.