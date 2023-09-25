# Add MFA with Email OTP

Email OTP is a One-Time Password (OTP) sent to the user's verified email address, which the user must submit during login (as an additional authentication step). This password is typically valid for a very short period.

During Email OTP authentication, the user is required to access the verified email account within a short time span to get the OTP. This prevents unauthorized users from accessing the OTP and thereby adds an extra layer of security to the authentication process.

Follow the instructions given below to configure Multi-Factor Authentication (MFA) using Email OTP in {{ product_name }}.

## Prerequisites
To get started, you need to [register an application with {{ product_name }}](../../guides/applications/). You can register your own application or use one of the [sample applications](../../get-started/try-samples/) provided.

!!! note "Info"
    You can use Email OTP for multi-factor authentication only if a previous authentication step is configured with **username and password** or another factor that can validate user credentials.
  
## Set up Email OTP
{{ product_name }} has some default settings for email OTP, which are sufficient for most cases. If required, you can change the default settings, as explained below.

To update the default Email OTP settings:

1. On the {{ product_name }}, go to **Connections** and select **Email OTP**.
2. Update the following parameters in the **Settings** tab:

    ![Setup email OTP in {{ product_name }}](../../../assets/img/guides/mfa/emailotp/setup-email-otp.png){: width="600"}

    <table>
      <tr>
        <th>Field</th>
        <th>Description</th>
      </tr>
      <tr>
        <td>Email OTP expiry time</td>
        <td>Specifies the expiry time of the OTP. The generated OTP will not be valid after this expiry time.</td>
      </tr>
      <tr>
        <td>Use only numeric characters for OTP</td>
        <td>
            Specifies whether to use only numeric characters in the OTP. If this is selected, the generated OTP contains only digits (0-9).
            If this option is not selected, the OTP will contain alphanumeric characters.
        </td>
      </tr>
      <tr>
        <td>Email OTP length</td>
        <td>Specifies the number of characters allowed in the OTP.</td>
      </tr>
    </table>
3. Once you update the Email OTP settings, click **Update**.

## Enable Email OTP for an app
To enable Email OTP for MFA, you need to add **Email OTP** in the authentication flow of the application.

Follow the steps given below.

1. On the {{ product_name }} Console, go to **Applications**.
2. Select the application to which you wish to add Email OTP.
3. Go to the **Sign-in Method** tab of the application and:

      - If you don't have a customized login flow, you can click **Add Email OTP as a second factor**.

        ![Add Email OTP authenticator](../../../assets/img/guides/mfa/emailotp/add-email-otp-authenticator.png){: width="600"}

        This opens the customized login flow with TOTP as a second-factor authenticator:

      - If you have an already customized login flow, you can add a second step and add TOTP as the authenticator.

        ![Customize the login flow](../../../assets/img/guides/mfa/totp/view-totp-authenticator.png){: width="600"}

    !!! note "Enable backup codes"
        Once the Email OTP authenticator is added, select **Enable backup codes**. This allows users to use their backup codes to log in to the application when they cannot obtain the required MFA codes.

        ![Enable backup codes for email otp authenticator](../../../assets/img/guides/mfa/emailotp/enable-backup-codes.png){: width="500"}

        Learn more about [configuring backup codes for business users](../../guides/user-self-service/manage-backup-codes/).

4. Click **Update** to save your changes.

## How it works

When Email OTP is enabled in the login flow of your application, the application user will be prompted with the Email OTP authentication step once the first authentication step is completed. Given below are the high-level steps that follow:

1. {{ product_name }} sends the OTP to the user's verified email address.
2. {{ product_name }} prompts the user to enter the OTP code.
  
   ![Authenticate with email OTP in {{ product_name }}](../../../assets/img/guides/mfa/emailotp/enter-email-otp.png){: width="300"}

3. If required, the user can request {{ product_name }} to resend the OTP. The new OTP invalidates the previously sent OTP.
4. The user enters the OTP and clicks **Continue**.
5. If the authentication is successful, the user can access the application.