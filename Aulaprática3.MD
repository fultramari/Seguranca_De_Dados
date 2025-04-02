## Tarefa 1: 

#include <stdio.h>
#include <openssl/bn.h>

#define NBITS 256

//p = F7E75FDC469067FFDC4E847C51F452DF
//q = E85CED54AF57E53E092113E62F436F4F
//e = 0D88C3

void printBN(char *msg, BIGNUM *a) {
    char *number_str = BN_bn2hex(a);
    printf("%s %s\n", msg, number_str);
    OPENSSL_free(number_str);
}

int main() {
    BN_CTX *ctx = BN_CTX_new();
    BIGNUM *p = BN_new();
    BIGNUM *q = BN_new();
    BIGNUM *n = BN_new();
    BIGNUM *totiente = BN_new();
    BIGNUM *d = BN_new();
    BIGNUM *e = BN_new();

    // Inicializa p, q, n 
    BN_hex2bn(&p,"F7E75FDC469067FFDC4E847C51F452DF");
    BN_hex2bn(&q,"E85CED54AF57E53E092113E62F436F4F"); 
    BN_hex2bn(&e, "0D88C3");

    // n = p * q
    BN_mul(n, p, q, ctx);
    printBN("p * q = ", n);
    
    // totiente = (p-1) * (q-1)
    BIGNUM *p_minus_1 = BN_new();
    BIGNUM *q_minus_1 = BN_new();
    BN_sub(p_minus_1, p, BN_value_one());
    BN_sub(q_minus_1, q, BN_value_one());  
    BN_mul(totiente, p_minus_1, q_minus_1, ctx);

    // D = e elevado -1 * mod (totiente)
    BN_mod_inverse(d, e, totiente, ctx);
    printf("Valor de D: ");
    printBN("", d);

    // Liberar memória
    BN_free(p);
    BN_free(q);
    BN_free(n);
    BN_free(e);
    BN_free(d);
    BN_free(p_minus_1);
    BN_free(q_minus_1);
    BN_free(totiente);
    BN_CTX_free(ctx);

    return 0;
}



## TAREFA 2
#include <stdio.h>
#include <openssl/bn.h>

#define NBITS 256

//p = F7E75FDC469067FFDC4E847C51F452DF
//q = E85CED54AF57E53E092113E62F436F4F
//e = 0D88C3

//n = DCBFFE3E51F62E09CE7032E2677A78946A849DC4CDDE3A4D0CB81629242FB1A5
//e = 010001 (decimal 65537)
//M = A grin without a cat!
//d = 74D806F9F3A62BAE331FFE3F0A68AFE35B3D2E4794148AACBC26AA381CD7D30D

void printBN(char *msg, BIGNUM *a) {
    char *number_str = BN_bn2hex(a);
    printf("%s %s\n", msg, number_str);
    OPENSSL_free(number_str);
}

int main() {
    BN_CTX *ctx = BN_CTX_new();
    BIGNUM *n = BN_new();
    BIGNUM *totiente = BN_new();
    BIGNUM *d = BN_new();
    BIGNUM *e = BN_new();

    // Inicializa p, q, n 
    BN_hex2bn(&n,"DCBFFE3E51F62E09CE7032E2677A78946A849DC4CDDE3A4D0CB81629242FB1A5");
    BN_dec2bn(&e, "12345678901112231223");

   
    
    // totiente = (p-1) * (q-1)
    BIGNUM *p_minus_1 = BN_new();
    BIGNUM *q_minus_1 = BN_new();
    BN_sub(p_minus_1, p, BN_value_one());
    BN_sub(q_minus_1, q, BN_value_one());  
    BN_mul(totiente, p_minus_1, q_minus_1, ctx);

    // D = e elevado -1 * mod (totiente)
    BN_mod_inverse(d, e, totiente, ctx);
    printf("Valor de D: ");
    printBN("", d);
    
    
    
    

    // Liberar memória
    BN_free(p);
    BN_free(q);
    BN_free(n);
    BN_free(e);
    BN_free(d);
    BN_free(p_minus_1);
    BN_free(q_minus_1);
    BN_free(totiente);
    BN_CTX_free(ctx);

    return 0;
}
