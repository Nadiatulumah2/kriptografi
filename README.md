# kriptografi
Nama : Nadiatul umah

NIM : 312210500

Kelas : Ti.22.A5

# def create_matrix(key):
    key = ''.join(sorted(set(key), key=key.index))  # remove duplicates
    key = key.replace('J', 'I')  # replace J with I
    alphabet = 'ABCDEFGHIKLMNOPQRSTUVWXYZ'
    matrix = key + ''.join(filter(lambda x: x not in key, alphabet))
    return [matrix[i:i + 5] for i in range(0, 25, 5)]

# def prepare_text(text):
    text = text.replace(' ', '').upper().replace('J', 'I')
    prepared = []
    i = 0
    while i < len(text):
        a = text[i]
        b = text[i + 1] if i + 1 < len(text) else 'X'
        if a == b:
            prepared.append(a + 'X')
            i += 1
        else:
            prepared.append(a + b)
            i += 2
    return prepared

# def encrypt(plaintext, key):
    matrix = create_matrix(key)
    pairs = prepare_text(plaintext)
    ciphertext = ''
    for a, b in pairs:
        row_a, col_a = divmod(matrix.index(a), 5)
        row_b, col_b = divmod(matrix.index(b), 5)
        if row_a == row_b:
            ciphertext += matrix[row_a][(col_a + 1) % 5]
            ciphertext += matrix[row_b][(col_b + 1) % 5]
        elif col_a == col_b:
            ciphertext += matrix[(row_a + 1) % 5][col_a]
            ciphertext += matrix[(row_b + 1) % 5][col_b]
        else:
            ciphertext += matrix[row_a][col_b]
            ciphertext += matrix[row_b][col_a]
    return ciphertext

# def decrypt(ciphertext, key):
    matrix = create_matrix(key)
    pairs = prepare_text(ciphertext)
    plaintext = ''
    for a, b in pairs:
        row_a, col_a = divmod(matrix.index(a), 5)
        row_b, col_b = divmod(matrix.index(b), 5)
        if row_a == row_b:
            plaintext += matrix[row_a][(col_a - 1) % 5]
            plaintext += matrix[row_b][(col_b - 1) % 5]
        elif col_a == col_b:
            plaintext += matrix[(row_a - 1) % 5][col_a]
            plaintext += matrix[(row_b - 1) % 5][col_b]
        else:
            plaintext += matrix[row_a][col_b]
            plaintext += matrix[row_b][col_a]
    return plaintext

# Contoh penggunaan
key = "TEKNIK INFORMATIKA"
plaintexts = [
    "GOOD BROOM SWEEP CLEAN",
    "REDWOOD NATIONAL STATE PARK",
    "JUNK FOOD AND HEALTH PROBLEMS"
]

# for text in plaintexts:
    encrypted = encrypt(text, key)
    decrypted = decrypt(encrypted, key)
    print(f"Plaintext: {text}")
    print(f"Ciphertext: {encrypted}")
    print(f"Decrypted: {decrypted}")
    print()

![Screenshot (262)](https://github.com/user-attachments/assets/9d719743-e3c8-406a-a882-44184e227140)

![Screenshot (263)](https://github.com/user-attachments/assets/7d84ee1b-c2d7-4c8b-894f-e7b077493cca)

![Screenshot (264)](https://github.com/user-attachments/assets/5bf7d0f9-f660-4cbf-952c-ff9e2191133b)

![Screenshot (265)](https://github.com/user-attachments/assets/775b3f60-4aac-4f1e-8651-f64e145ad8c1)

![Screenshot (266)](https://github.com/user-attachments/assets/c3a3d994-98f7-4ca3-84f3-cf7ea0e986db)

![Screenshot (267)](https://github.com/user-attachments/assets/b34ef3ce-cee3-47cd-8385-50f648a9caba)

![Screenshot (268)](https://github.com/user-attachments/assets/01b07f1c-e628-49c6-b0a9-2cb0bd93a56a)

![Screenshot (269)](https://github.com/user-attachments/assets/cd5a2612-02f4-41e6-8694-569943abe5e1)










