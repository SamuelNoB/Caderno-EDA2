# Revisão de ponteiros
## tipos e tamanhos de dados
Tipo    | Bytes
--------|----------
`char`  |   1byte 
`int`   |   4bytes
`float` |   4bytes
`double`|   8bytes
`long`  |   8bytes

## Ponteiro básico
Ponteiro é denominado pelo `*`. Ele armazena a **referencia de memória** para um outro lugar.

EX:
~~~C
int main() {
    int a, *b;

    a = 0;
    b = &a;     // 'b' armazena o endereço de 'a'
    *b = 15;    // atravez de 'b' o valor de 'a' foi alterado. Logo: a = 15;

    return 0;
}
~~~

É possível armazenar referências para vetores com ponteiros. É também possível caminhar por um vetor atravez do ponteiro a ele relacionado
~~~C
    int vetor[10] = {0, 2, 2, 3, 4, 5, 6, 7, 8, 9};
    int *ponteiro, variavel;

    ponteiro = vetor;  // a var ponteiro irá armazenar o endereço de memoria da posição zero do vetor
    ponteiro = &vetor[0]; // também pode ser escrito desta forma

    variavel = *(ponteiro+1);   // 'variavel' vai receber o valor contido no vetor[1]
~~~

## Passagem de parâmetro por cópia e por referência

### Parâmetro por cópia
Dentro da pilha da memória, quando uma função é chamada possuindo parâmetros por cópia, as variáveis e seus valores são copiados para uma nova variável dentro do escopo da função.

### Parâmetro por referência

Ná pilha de memória uma nova variável é criada contendo o endereço de memória para outra variável. Um endereço de memória deve ser passado para o parâmetro. E qualquer alteração feita no valor da variável do parâmetro também será refletida na variável original

EX:
~~~C
void parametro_referencia(int *a){
    *a = *a+10  // aqui também significa que x = x + 10; dentro do escopo da função main()

    a = 20;   // o endereço que a possuia armazenado foi alterado para o endereço 20
}

void vetor_estatico(int *vetor, int tamanho){
    vetor[0] = 1;  // a variavel vet[0] na main recebe o valor 1
    vetor[1] = 2;   // vet[1] = 2;
    // ou

    *vetor = 2;         // vetor[0] = 2; ==> vet[0] = 2; 
    *(vetor+1) = 3;     // vetor[1] = 3; ==> vet[1] = 3; 

}

int main(){
    int x=15, vet[4];
    parametro_referencia(&x);  // endereço de memória de 'x' é passado para o ponteiro 'a'
    vetor_estatico(vet, 4)
}
~~~