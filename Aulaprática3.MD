## Tarefa 1: 
```
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

```

## TAREFA 2
```
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

```


## Copiando de novo a tarefa 1 por remorso
```
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
```
    BN_CTX_free(ctx);

    return 0;
}

## TAREFA 3
6) Qual foi o código C que você usou para verificar a assinatura? Explique os valores que você usou para as variáveis e as contas feitas com eles.  

Assinatura do certificado 0 (S = signature):  
490f1f133577f2997b079498d7b413b45773353d2f9712bd66f758b  
70386f41826585741d2b290136f0184009bd01f2609b110034d3f731f497d7  
80032737291b96f038154291b426482f2d97203095fb8b16267b04548  
608943354d1fd3759d109d907f340d6887f609793921fdf9f20634b4  
6b2878fd0559b6d647177034d503b949575f3791f3342321fd79  
b10785030144d7d0909214464076b504f11b5030038b6f97d4d47007  
04625b50f555bf47928df262b4bd5f489525792d551f6d9739137597b68868ddf071

Módulo (valor de n):
A5F2D1A55214C1B80178122F9A039D43EA96CEF33DAD45BA29382AA4DF4936B3D50EEE70E2E5FBE9A0CBE6B442C34282E9D8DDF5D3C1698A3190018F8F8AE4E0B3C8D22E68065D1BB54DE3E7AE216AC74BA303C9CA51DF547FA33ED195ED1BC6FEE6BC45015E83FF50889C62E3378DEAC854283A32C7EF03D65FF7AC16F80CB9C049A61B086634B49350BC0A14B633AF13688AB01F81216A3AF792138B63AE916E22E6588FF139F3BB694F5E2C3E494AF22B9099B7DEDF625DB19F6450A8003A34E76851F74B5C5A28062C1C794E0257289DDD930E779301D53507A7EF7CA1DCF2559C18BD65BB36A05F2F28B683138CB2C020CBAC31E18B29C84FC14BC7CAB7

e (expoente público):
Exponent: 65537


Hash do certificado 0:
9fd08871aeae51593521355f18f47601a49436e5104cb329dbc90eed3585df6d 




Por meio do código abaixo, utilizando os valores de n,e, e da mensagem a ser criptografada(certificado, valor de S), o hash obtido foi:
01FFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFF003031300D060960864801650304020105000420"9FD08871AEAE51593521355F18F47601A49436E5104CB329DBC90EED3585DF6D"


```
#include <stdio.h>
#include <openssl/bn.h>
#define NBITS 256
void printBN(char *msg, BIGNUM * a)  //print bignum como hexadecimal
{
	char * number_str = BN_bn2hex(a);
	printf("%s %s\n", msg, number_str);
	OPENSSL_free(number_str);
}
int main ()
{
	BN_CTX *ctx = BN_CTX_new();
	BIGNUM *s = BN_new();
	BIGNUM *e = BN_new();
	BIGNUM *d = BN_new();
	BIGNUM *n = BN_new();
	BIGNUM *c = BN_new();
	BIGNUM *res = BN_new();

	//Inicializa a, b, n
	
	BN_hex2bn(&n, "A5F2D1A55214C1B80178122F9A039D43EA96CEF33DAD45BA29382AA4DF4936B3D50EEE70E2E5FBE9A0CBE6B442C34282E9D8DDF5D3C1698A3190018F8F8AE4E0B3C8D22E68065D1BB54DE3E7AE216AC74BA303C9CA51DF547FA33ED195ED1BC6FEE6BC45015E83FF50889C62E3378DEAC854283A32C7EF03D65FF7AC16F80CB9C049A61B086634B49350BC0A14B633AF13688AB01F81216A3AF792138B63AE916E22E6588FF139F3BB694F5E2C3E494AF22B9099B7DEDF625DB19F6450A8003A34E76851F74B5C5A28062C1C794E0257289DDD930E779301D53507A7EF7CA1DCF2559C18BD65BB36A05F2F28B683138CB2C020CBAC31E18B29C84FC14BC7CAB7");
	BN_hex2bn(&e, "010001");
	BN_hex2bn(&s, "490f1f1335e77f2997b079498de7eb4e13b45e773353cd2fa97a12becd66f7ec58b70386fe41826585a741d2b2901a36cf018acc40c09bd01ef2609b11003c4dc3fa7ce31fc497d7800327c37a291bcea9a6f0381e54291b426482fec2de9a720e3095cfb8b1c6267b04548ae6089433e54ada1fd37c59d109cd907fc340de6c8e87f6e097c939a21afdf9ef206c34b46b2878fd0ac559b6ed647177034dcaa5c03cb949575ecf379e1f3ce34ec232c1fda7eae9b10785c0e30144d7de090ac92aa14c46ee4076ccb504f11be5030038ceb6f97cd4d4700704c625b50fee555bf47928df26a2b4bd5f489ca525792d551af6d973ae9137597b68aa868ddf07e1");
	
	// res hash = S^e mod n
	BN_mod_exp(res, s, e, n, ctx);
	printBN("hash: ", res);
	

	return 0;
}


```

Explicação: O código, de forma geral, pega o hash criptografado pela chave privada e o descriptografa com a chave pública. Caso ele seja coerente com o Hash do certificado 0, quer dizer que é seguro e os outros certificados podem ser confiáveis. Para essa conta, foi necessário obter n(módulo) e o e (expoente público), que está presente no certificado 1, e aplicar o algorítmo RSA na assinatura de C0.

7) Houve preenchimento na mensagem (padding)? Caso sim, mostre, na assinatura decodificada, quais são os bytes originais e quais são os bytes do preenchimento.  
R: Houve preenchimento sim, seguindo a seguinte lógica:
    - 01 — Início do padding (indica assinatura).
    - Vários FF — Padding em si.
    - 00 — Separador.
    - 30 31 ... — Um ASN.1 DER encoding que identifica o algoritmo hash usado.
    - 04 20 ... — Prefixo 04 20 indica que os próximos 32 bytes são o hash (isso é um OCTET STRING de 32 bytes).
    - 9F D0 88 71 ... DF 6D — Este é o hash SHA-256 da mensagem original.



8) A RNP, Trusted Root, e GlobalSign são autoridades de certificação (CAs). Qual é a
função de uma CA?
    - Emissão de certificados: Vincula uma identidade (ex: conferenciaweb.rnp.br) a uma chave pública.
    - Assinatura digital: Usa sua chave privada para assinar certificados, garantindo autenticidade.
    - Hierarquia de confiança: Certificados raiz (ex: GlobalSign) são pré-instalados em sistemas/browsers.
    - Cadeia de certificação valida certificados intermediários (ex: RNP → Trusted Root → GlobalSign).

9) Explique por que o certificado 0 (Conferência Web) pode ser considerado seguro a partir dos certificados 1, 2 e 3.

R: A segurança é garantida pela cadeia de confiança:  
    - Certificado 3 (GlobalSign): Autoassinado, pré-instalado em navegadores (confiança global).  
    - Certificado 2 (Trusted Root): Assinado pela GlobalSign (chave privada da GlobalSign valida o Certificado 2).  
    - Certificado 1 (RNP): Assinado pela Trusted Root (chave privada da Trusted Root valida o Certificado 1).  
    - Certificado 0 (Conferência Web): Assinado pela RNP (chave privada da RNP valida o Certificado 0).

** Fluxo de Validação **  
    - O navegador verifica a assinatura do Certificado 0 usando a chave pública da RNP (extraída do Certificado 1).  
    - A chave pública da RNP é validada pelo Certificado 1, assinado pela Trusted Root.  
    - A Trusted Root é validada pelo Certificado 2, assinado pela GlobalSign.  
    - A GlobalSign é confiável por ser um certificado raiz pré-instalado.

Conclusão
Se todas as assinaturas na cadeia são válidas, o Certificado 0 é considerado seguro.
Um atacante não pode falsificá-lo sem a chave privada da RNP (ou de alguma CA superior).
