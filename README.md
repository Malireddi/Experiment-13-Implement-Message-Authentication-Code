# Exp-13-Implement-Message-Authentication-Code
# AIM:
To generate and verify a Message Authentication Code (MAC) for ensuring the integrity and authenticity of a message using a simple XOR operation.

# DESIGN STEPS:
Step 1:
Input a secret key and a message from the user.

Step 2:
Generate the MAC by applying a simple XOR operation between the secret key and the message.

Step 3:
The MAC is computed by repeating the key or message as necessary.

Step 4:
The user can input a received MAC, and the program verifies whether the received MAC matches the computed MAC.

Step 5:
The authenticity of the message is confirmed if the MACs match.

# PROGRAM:
#include <stdio.h>
#include <string.h>

#define MAC_SIZE 32 // Define MAC size in bytes

// Function to compute a simple MAC using XOR
void computeMAC(const char *key, const char *message, char *mac) {
    int key_len = strlen(key);     // Length of the secret key
    int msg_len = strlen(message);  // Length of the message
    
    // XOR the key and message, repeating if necessary
    for (int i = 0; i < MAC_SIZE; i++) {
        mac[i] = key[i % key_len] ^ message[i % msg_len]; // Simple XOR operation
    }
}

// Main function to execute the MAC computation and verification
int main() {
    char key[100];                  // Buffer for the secret key
    char message[100];              // Buffer for the message
    char mac[MAC_SIZE];             // Buffer for the computed MAC
    unsigned char receivedMAC[MAC_SIZE]; // Buffer for the received MAC

    // Step 1: Input secret key
    printf("Enter the secret key: ");
    scanf("%99s", key); // Read up to 99 characters to prevent overflow

    // Step 2: Input the message
    printf("Enter the message: ");
    scanf("%99s", message); // Read up to 99 characters to prevent overflow

    // Step 3: Compute the MAC using the provided key and message
    computeMAC(key, message, mac);

    // Step 4: Display the computed MAC in hexadecimal format
    printf("Computed MAC (in hex): ");
    for (int i = 0; i < MAC_SIZE; i++) {
        printf("%02x", (unsigned char)mac[i]); // Print each byte as two-digit hex
    }
    printf("\n");

    // Step 5: Input the received MAC for verification
    printf("Enter the received MAC (as hex): ");
    for (int i = 0; i < MAC_SIZE; i++) {
        scanf("%2hhx", &receivedMAC[i]); // Read hex values directly into the array
    }

    // Step 6: Compare the computed MAC with the received MAC
    if (memcmp(mac, receivedMAC, MAC_SIZE) == 0) {
        printf("MAC verification successful. Message is authentic.\n");
    } else {
        printf("MAC verification failed. Message is not authentic.\n");
    }

    return 0; // Indicate that the program finished successfully
}

# OUTPUT:
![image](https://github.com/user-attachments/assets/e1bd23dd-f654-4fe2-aab2-e6e3e502714f)





# RESULT:
The program for generating and verifying a Message Authentication Code (MAC) was executed successfully, demonstrating the integrity and authenticity of the message through a simple XOR-based MAC.
