# Nama: Nadiatul umah

# Generate preparekey  
def prepare_key(key):
  key = key.upper().replace("J", "I")
  key_matrix = []
  for char in key:
    if char not in key_matrix and char.isalpha():
      key_matrix.append(char)
  for char in range(ord('A'), ord('Z') + 1):
    char = chr(char)
    if char not in key_matrix and char != 'J':
      key_matrix.append(char)
  matrix = [key_matrix[i:i+5] for i in range(0, 25, 5)]
  return matrix

# find position matrix 
def find_position(matrix, char):
  for i in range(5):
    for j in range(5):
      if matrix[i][j] == char:
        return (i, j)
  return None

#  encrypt plaintext
def encrypt(plaintext, key):
  matrix = prepare_key(key)
  plaintext = plaintext.upper().replace("J", "I")
  plaintext = "".join(filter(str.isalpha, plaintext))

  if len(plaintext) % 2 != 0:
    plaintext += 'X'

  ciphertext = ""
  for i in range(0, len(plaintext), 2):
    char1 = plaintext[i]
    char2 = plaintext[i+1]

    row1, col1 = find_position(matrix, char1)
    row2, col2 = find_position(matrix, char2)

    if row1 == row2:
      ciphertext += matrix[row1][(col1 + 1) % 5]
      ciphertext += matrix[row2][(col2 + 1) % 5]
    elif col1 == col2:
      ciphertext += matrix[(row1 + 1) % 5][col1]
      ciphertext += matrix[(row2 + 1) % 5][col2]
    else:
      ciphertext += matrix[row1][col2]
      ciphertext += matrix[row2][col1]

  return ciphertext


# decrypt ciphertext 
def decrypt(ciphertext, key):
  matrix = prepare_key(key)
  plaintext = ""

  for i in range(0, len(ciphertext), 2):
    char1 = ciphertext[i]
    char2 = ciphertext[i+1]

    row1, col1 = find_position(matrix, char1)
    row2, col2 = find_position(matrix, char2)

    if row1 == row2:
      plaintext += matrix[row1][(col1 - 1) % 5]
      plaintext += matrix[row2][(col2 - 1) % 5]
    elif col1 == col2:
      plaintext += matrix[(row1 - 1) % 5][col1]
      plaintext += matrix[(row2 - 1) % 5][col2]
    else:
      plaintext += matrix[row1][col2]
      plaintext += matrix[row2][col1]

  return plaintext




![potoo](https://github.com/user-attachments/assets/6c2cb8a8-3678-4b91-92bc-9647c0a5fdb7)
