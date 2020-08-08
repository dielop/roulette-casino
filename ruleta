#include <stdio.h>
#include <stdlib.h>
#include <unistd.h>


//MACROS
#define MAX 1
#define MAXROUNDS 20
#define MNUM 37

//FUNCIONES:
void welcome();//Bienvenida.
int rounds();//Cantidad de rondas.
int bets();//Cantidad de apuestas.
float valorfich();//Valor de la ficha que se apuesta y cantidad.
void NUM(float, int); //Funcion de un numero.
void DOC(float, int); //Funcion de docenas.
void COLUM(float, int); //Funcion de columnas.
void COLOR(float, int, int); //Funcion de color.
void FALTAOPASA(float, int); //Funcion de falta/pasa.
void NROPARIMPAR(float, int); //Funcion de numero par/impar.
int premio(int );//Giro de bola y numero ganador.
void winandloss(int, int); //Pagos de la mesa
void showwal(int);//Impresion de pagos.
void globaltable();//Calcula la sumatoria de ganancias y perdidas al finalizar todas las rondas.
int colorcontred(int);//Funcion que retorna cada vez que la bola cae en un numero rojo (Resultados 5).
int colorcontblack(int);//Funcion que retorna cada vez que la bola cae en un numero negro (Resultados 5).
int informar(int ); //Informa las rondas que salio 0 o multiplo de 10 (Resultados 6).
int nroprimo(int ); //cuenta numeros primos (Resultados 8).





//VARIABLES GLOBALES
int RUL[36][10] = {0,0};//Paño ruleta con apuestas.
int ALMACEN[10] = {0};//Almacena la apuesta realizada.
float ALMACAPU[200] = {0};//Almacena el monto de la apuesta realizada.
float ALMAWIN[200] = {0}; //Almacena lo que gana por apuesta.
float BANK[20] = {0};//Almacena si se apuesta a rojo o negro.








int main()
{
    int rondas, apuestas, j; //Rondas a efectuar y apuestas.
    int r;//contador de rondas.
    int fortuna;//Numero ganador.
    float totalbet;//monto total de las apuestas.
    int choice; //Opcion que se aposto.
    int ALMAC[10] = {0};//Almacena la eleccion para generar luego la restriccion con el while mas arriba
    float s = 0;//Cuenta apuestas para el resultado 1.
    float falseprom; //Promedio de apuestas por ronda (Resultados 1).
    float MAYORAPUESTA[10] = {0};//Almacena la mayor de las apuestas.(Resultados 2).
    float ALBET[20] = {0}; //Almacena por ronda la mayor apuesta.(Resultados 2).
    float numeromayorronda; //Variable donde se define la mayor apuesta de todas las rondas.(Resultados 2).
    int posnummayor = 0; //Ronda de la apuesta de mayor valor (Resultados 2).
    float bankred = 0, bankblack = 0;//Cuenta las apuestas a rojos y a negros para (resultados 3).
    float porcentualrojo, porcentualnegro;  //Apuestas porcentuales a rojos y a negros para (resultados 3).
    float contadorpthree = 0; //Cuenta cada vez que se apuesta a color. (Resultados 3).
    int cuentarojo = 0, cuentanegro = 0; //Contador de rojos y negros para saber si salio mas de 5 veces la bola en uno o en otro (resultados 5).
    int contpremios = 0;//Cuenta si salio alguna vez el 0 o multiplos de 10 por ronda. (Resultados 6).
    int primos = 0; //cuenta nros primos. (Resultados 8).





//Bienvenida a la RULETA

    welcome();

//Solicito al usuario que indique la cantidad de rondas que quiere jugar.

    rondas = rounds();

//Rondas que se juega

    for(r=0; r<rondas; r++)
    {
        printf("\nRONDA %d: ", r+1);

        apuestas = bets();

//Apuestas realizadas por ronda

        for(j=0; j<apuestas; j++)
        {
            printf("\nApuesta %d: ", j+1);
            totalbet = valorfich();

//Almaceno la apuesta de mayor valor

            if(MAYORAPUESTA[0]<=totalbet)
            {
                MAYORAPUESTA[0]=totalbet;
            }

//Almaceno cuanto es lo que apuesto

            ALMACAPU[j] = totalbet;

            do
            {
                do
                {
                    printf("\n Digite la opcion a apostar: ");
                    printf("\n 1) Apostar a un Nº                                       (paga 35 a 1).");
                    printf("\n 2) Apostar a una docena                                   (paga 3 a 1).");
                    printf("\n 3) Apostar a una columna                                  (paga 3 a 1).");
                    printf("\n 4) Apostar al color                                       (paga 2 a 1).");
                    printf("\n 5) Apostar a falta o pasa                                 (paga 2 a 1).");
                    printf("\n 6) Apostar a un Nº par o impar                            (paga 2 a 1).");
                    printf("\n ---> ");
                    scanf("%d", &choice);
                }
                while(choice<=6 && choice>=4 && choice==ALMAC[r]);
            }
            while(choice<=0 || choice>6);

//Almacena la eleccion para generar luego la restriccion con el while mas arriba

            ALMAC[r] = choice;

//Almacena la leccion

            ALMACEN[j] = choice;

//Cuento las veces que se apuesta a color

            if(ALMACEN[j]==4)
            {

                contadorpthree++;

            }


            switch(choice)
            {
            case 1:
            {
                NUM(totalbet, j);
                break;
            }

            case 2:
            {
                DOC(totalbet, j);
                break;
            }
            case 3:
            {
                COLUM(totalbet, j);
                break;
            }

            case 4:
            {
                COLOR(totalbet, j, r);
                break;
            }
            case 5:
            {
                FALTAOPASA(totalbet, j);
                break;
            }
            case 6:
            {
                NROPARIMPAR(totalbet, j);
                break;
            }

            }

        } /*Finaliza ciclo de apuestas.*/

//Numero que cae la bola

        fortuna = premio(r);

        printf("\nEl numero ganador es: %d\n", fortuna);

//Calculo de ganancias o perdidas por ronda(funcion tambien dentro)

        for(j=0; j<apuestas; j++)
        {

            winandloss(j, fortuna);

        }

//Impresion de ganancias o perdidas por ronda

        for(j=0; j<apuestas; j++)
        {
            showwal(j);

        }



//Funcion de Resultado punto 6.

        contpremios += informar(fortuna);

//Funcion de Resultado punto 8.

        primos += nroprimo(fortuna);


//Si en mas de 5 rondas la bola cayo en numeros de igual color

        cuentarojo += colorcontred(fortuna);

        cuentanegro += colorcontblack(fortuna);

//Cuenta apuestas para el resultado 1.

        for(j=0; j<apuestas; j++)
        {
            if(ALMACEN[j]!=0)
            {
                s++;
            }
        }


//Almacena la apuesta de mayor valor

        ALBET[r]=MAYORAPUESTA[0];


    } /*Finaliza ciclo de rondas.*/

//Ganancias totales y perdidas totales al finalizar todas las rondas

    globaltable();


//Promedio de apuestas por ronda (Resultados 1)


    falseprom = s/r;

    printf("\nHubo un promedio de %.2f apuestas por ronda", falseprom);


//Contador de apuestas a rojo y negro

    for(r=0; r<rondas; r++)
    {

        if(BANK[r]==1)
        {
            bankred++;
        }
        else if(BANK[r]==2)
        {
            bankblack++;
        }
    }


//Comparativa porcentual de apuestas ROJO vs NEGRO


    porcentualrojo = (bankred/contadorpthree)*100;
    porcentualnegro = (bankblack/contadorpthree)*100;

    printf("\nSe aposto %.2f por ciento al rojo y %.2f por ciento al negro.", porcentualrojo, porcentualnegro);



//Resultados numero 6 (premio igual a 0 o multiplo de 10)

    if(contpremios != 0)
    {
        printf("\nEn al menos 1 ronda salio el 0 o numeros multiplos de 10.");
    }
    else
    {
        printf("\nEn ninguna ronda salio el 0 o numero multiplo de 10.");
    }


    printf("\nLa bola cayo %d vez/veces en un numero primo.", primos);

    if(cuentarojo>5 || cuentanegro>5)
    {

        printf("\nLa bola cayo en mas de 5 rondas seguidas en numeros de igual color.");

    }
    else
    {

        printf("\nLa bola no cayo en mas de 5 rondas seguidas en numeros de igual color.");

    }

//Resultados numero 2 (Apuesta de mayor valor monetario y ronda que sucede)


    numeromayorronda = ALBET[0];

    for(r=0; r<rondas; r++)
    {
        if(ALBET[r]>numeromayorronda)
        {
            numeromayorronda = ALBET[r];
            posnummayor = r;
        }

    }


    printf("\nLa mayor apuesta fue %.2f en la ronda %d", numeromayorronda, posnummayor+1);






    return 0;
}




//Funcion bienvenida

void welcome()
{

    printf("********************************************\n");
    printf("  ¡Bienvenidos al simulador de la ruleta!\n");
    printf("********************************************\n");


}

//Funcion de rondas

int rounds()
{
    int rondas;

    do
    {
        printf("\nIngrese la cantidad de rondas que quiere jugar(MAX:20): ");
        scanf("%d", &rondas);
    }
    while(rondas<0 || rondas>MAXROUNDS);

    //Si no hay rondas indico que se termino el juego

    if(rondas == 0)
    {
        printf("\nFIN DEL JUEGO");
        printf("\nTodo los resultados emitidos bajo este enunciado son invalidados.\n");

        return 0;
    }

    return rondas;
}

//Funcion cantidad de apuestas

int bets()
{
    int i;

    do
    {
        printf("Ingrese la cantidad de apuestas(MAX=10): ");
        scanf("%d", &i);

    }
    while(i<0 || i>10);

    if(i == 0)
    {
        printf("\nFIN DEL JUEGO");
        printf("\nTodo los resultados emitidos bajo este enunciado son invalidados.\n");

        return 0;
    }

    return i;
}



void NUM(float a, int j)
{
    int b;

    do
    {
        printf("\nDigite el Nº colocado en la apuesta (0 a 36): ");
        scanf("%d", &b);
    }
    while(b<0 || b>36);

    RUL[b][j] = a;

}

void DOC(float a, int j)
{
    int b;
    int i;


    do
    {
        printf("\nDigite la opcion de docena a apostar.");
        printf("\n1 - 1era docena");
        printf("\n2 - 2da docena");
        printf("\n3 - 3era docena");
        printf("\n--> ");
        scanf("%d", &b);

    }
    while(b<1 || b>3);

    switch(b)
    {
    case 1:
    {
        for(i=1; i<=12; i++)
        {
            RUL[i][j] = a;
        }
        break;
    }
    case 2:
    {
        for(i=13; i<=24; i++)
        {
            RUL[i][j] = a;
        }
        break;
    }
    case 3:
    {
        for(i=25; i<=36; i++)
        {
            RUL[i][j] = a;
        }
        break;
    }
    }

}

void COLUM(float a, int j)
{
    int b;
    int i;

    do
    {
        printf("\nDigite la opcion de columna a apostar.");
        printf("\n1 - 1era columna.");
        printf("\n2 - 2da columna.");
        printf("\n3 - 3era columna.");
        printf("\n-->");
        scanf("%d", &b);
    }
    while(b<1 || b>3);

    switch(b)
    {
    case 1:
    {
        for(i=1; i<35; i+=3)
        {
            RUL[i][j] = a;
        }
        break;
    }
    case 2:
    {

        for(i=2; i<36; i+=3)
        {
            RUL[i][j] = a;
        }
        break;
    }
    case 3:
    {
        for(i=3; i<37; i+=3)
        {
            RUL[i][j] = a;
        }
        break;
    }
    }



}
void COLOR(float a, int j, int r)
{

    int x;

    {
        printf("\nDigite opcion a apostar: ");
        printf("\n1 - Color ROJO.");
        printf("\n2 - Color NEGRO.");
        printf("\n--> ");
        scanf("%d", &x);
    }
    while(x<1 || x>2);

    BANK[r] = x;

    switch(x)
    {
    case 1:
    {
        RUL[1][j] = a;
        RUL[3][j] = a;
        RUL[5][j] = a;
        RUL[7][j] = a;
        RUL[9][j] = a;
        RUL[12][j] = a;
        RUL[14][j] = a;
        RUL[16][j] = a;
        RUL[18][j] = a;
        RUL[19][j] = a;
        RUL[21][j] = a;
        RUL[23][j] = a;
        RUL[25][j] = a;
        RUL[27][j] = a;
        RUL[30][j] = a;
        RUL[32][j] = a;
        RUL[34][j] = a;
        RUL[36][j] = a;

        break;
    }

    case 2:
    {
        RUL[2][j] = a;
        RUL[4][j] = a;
        RUL[6][j] = a;
        RUL[8][j] = a;
        RUL[10][j] = a;
        RUL[11][j] = a;
        RUL[13][j] = a;
        RUL[15][j] = a;
        RUL[17][j] = a;
        RUL[20][j] = a;
        RUL[22][j] = a;
        RUL[24][j] = a;
        RUL[26][j] = a;
        RUL[28][j] = a;
        RUL[29][j] = a;
        RUL[31][j] = a;
        RUL[33][j] = a;
        RUL[35][j] = a;

        break;
    }

    }


}


void FALTAOPASA(float a, int j)
{
    int t, i;

    do
    {
        printf("\nDigite opcion a apostar: ");
        printf("\n1 - Apostar FALTA.");
        printf("\n2 - Apostar PASA.");
        printf("\n-->");
        scanf("%d", &t);
    }
    while(t<1 || t>2);

    switch(t)
    {
    case 1:
    {
        RUL[1][j] = a;
        RUL[2][j] = a;
        RUL[3][j] = a;
        RUL[4][j] = a;
        RUL[5][j] = a;
        RUL[6][j] = a;
        RUL[7][j] = a;
        RUL[8][j] = a;
        RUL[9][j] = a;
        RUL[10][j] = a;
        RUL[11][j] = a;
        RUL[12][j] = a;
        RUL[13][j] = a;
        RUL[14][j] = a;
        RUL[15][j] = a;
        RUL[16][j] = a;
        RUL[17][j] = a;
        RUL[18][j] = a;

        break;

    }
    case 2:
    {
        RUL[19][j] = a;
        RUL[20][j] = a;
        RUL[21][j] = a;
        RUL[22][j] = a;
        RUL[23][j] = a;
        RUL[24][j] = a;
        RUL[25][j] = a;
        RUL[26][j] = a;
        RUL[27][j] = a;
        RUL[28][j] = a;
        RUL[29][j] = a;
        RUL[30][j] = a;
        RUL[31][j] = a;
        RUL[32][j] = a;
        RUL[33][j] = a;
        RUL[34][j] = a;
        RUL[35][j] = a;
        RUL[36][j] = a;

        break;
    }

    }

}

void NROPARIMPAR(float a, int j)
{
    int t;

    do
    {
        printf("\nDigite opcion a apostar: ");
        printf("\n1 - Numeros PAR.");
        printf("\n2 - Numeros IMPAR.");
        printf("\n-->");
        scanf("%d", &t);
    }
    while(t<1 || t>2);

    switch(t)
    {
    case 1:
    {
        RUL[2][j] = a;
        RUL[4][j] = a;
        RUL[6][j] = a;
        RUL[8][j] = a;
        RUL[10][j] = a;
        RUL[12][j] = a;
        RUL[14][j] = a;
        RUL[16][j] = a;
        RUL[18][j] = a;
        RUL[20][j] = a;
        RUL[22][j] = a;
        RUL[24][j] = a;
        RUL[26][j] = a;
        RUL[28][j] = a;
        RUL[30][j] = a;
        RUL[32][j] = a;
        RUL[34][j] = a;
        RUL[36][j] = a;

        break;

    }
    case 2:
    {

        RUL[1][j] = a;
        RUL[3][j] = a;
        RUL[5][j] = a;
        RUL[7][j] = a;
        RUL[9][j] = a;
        RUL[11][j] = a;
        RUL[13][j] = a;
        RUL[15][j] = a;
        RUL[17][j] = a;
        RUL[19][j] = a;
        RUL[21][j] = a;
        RUL[23][j] = a;
        RUL[25][j] = a;
        RUL[27][j] = a;
        RUL[29][j] = a;
        RUL[31][j] = a;
        RUL[33][j] = a;
        RUL[35][j] = a;

        break;

    }
    }
}

//Giro de ruleta

int premio(int r)
{
    int prem;

    srand(getpid()+r);
    prem = rand()%37;


    return prem;

}

//Valor de apuesta

float valorfich()
{
    int bet, cantidad, totalapostado;

    do
    {
        printf("\nDigita el valor de las fichas a apostar:\n");
        printf("\n 1) $1.");
        printf("\n 2) $2.");
        printf("\n 5) $5.");
        printf("\n 10) $10.");
        printf("\n 50) $50.");
        printf("\n 100) $100.");
        printf("\n ---> ");
        scanf("%d", &bet);
    }
    while(bet!=1 && bet!=2 && bet!=5 && bet!=10 && bet!=50 && bet!=100);


    printf("\nDigita la cantidad de fichas a apostar:\n");
    scanf("%d", &cantidad);


    totalapostado = bet * cantidad;

    printf("\nUsted apostara %d creditos.\n", totalapostado);

    return totalapostado;

}

//Pagos de ganancias o perdidas

void winandloss(int apu, int fortuna)
{
    int n;

    switch(ALMACEN[apu])
    {
    case 1:
    {
        for(n=0; n<MNUM; n++)
        {

            if(RUL[n][apu]>0 && n==fortuna)
            {
                ALMACAPU[apu]=0;
                ALMAWIN[apu]=(RUL[n][apu])*35;
            }
        }

        break;
    }
    case 2:
    {
        for(n=0; n<MNUM; n++)
        {

            if(RUL[n][apu]>0 && n==fortuna)
            {
                ALMACAPU[apu]=0;
                ALMAWIN[apu]=(RUL[n][apu])*3;
            }
        }

        break;
    }
    case 3:
    {
        for(n=0; n<MNUM; n++)
        {

            if(RUL[n][apu]>0 && n==fortuna)
            {
                ALMACAPU[apu]=0;
                ALMAWIN[apu]=(RUL[n][apu])*3;
            }
        }

        break;

    }
    case 4:
    {
        for(n=0; n<MNUM; n++)
        {

            if(RUL[n][apu]>0 && n==fortuna)
            {
                ALMACAPU[apu]=0;
                ALMAWIN[apu]=(RUL[n][apu])*2;
            }
        }
        break;
    }
    case 5:
    {

        for(n=0; n<MNUM; n++)
        {

            if(RUL[n][apu]>0 && n==fortuna)
            {
                ALMACAPU[apu]=0;
                ALMAWIN[apu]=(RUL[n][apu])*2;
            }
        }
        break;

    }
    case 6:
    {
        for(n=0; n<MNUM; n++)
        {

            if(RUL[n][apu]>0 && n==fortuna)
            {
                ALMACAPU[apu]=0;
                ALMAWIN[apu]=(RUL[n][apu])*2;
            }
        }
        break;
    }
    }
}

//Impresion de las ganancias o perdidas por ronda.

void showwal(int apu)
{
    if(ALMAWIN[apu]==0)
    {
        printf("\nLa mesa ha ganado: %.2f creditos", ALMACAPU[apu]);
    }
    else
    {
        printf("\nLa mesa ha perdido: %.2f creditos", ALMAWIN[apu]);
    }

}

//Funcion de ganancias o perdidas globales

void globaltable()
{
    int o;//Iniciador
    float globalbetwin;//Ganancia total de la mesa
    float globalbetloss;//Perdida total de la mesa

    for(o=0; o<201; o++)
    {

        globalbetwin += ALMACAPU[o];

    }

    for(o=0; o<201; o++)
    {

        globalbetloss += ALMAWIN[o];

    }


    if(globalbetwin>globalbetloss)
    {
        printf("\nMesa ganadora!!!");
    }
    else if(globalbetwin<globalbetloss)
    {
        printf("\nMesa en problemas ;)");
    }
    else
    {
        printf("\nMesa no conforme");
    }

}



//Funcion que retorna cada vez que la bola cae en un numero rojo (Resultados 5).

int colorcontred(int nro)
{
    int contadorrojo = 0;


    if(nro==1 || nro==3 || nro==5 || nro==7 || nro==9 || nro==12)
    {

        contadorrojo++;

    }
    else if(nro==14 || nro==16 || nro==18 || nro==19 || nro==21)
    {

        contadorrojo++;

    }
    else if(nro==23 || nro==25 || nro==27 || nro==30 || nro==32 || nro==34 || nro==36)
    {

        contadorrojo++;

    }
    else
    {

        contadorrojo = 0;

    }

    return contadorrojo;

}

//Funcion que retorna cada vez que la bola cae en un numero negro (Resultados 5).

int colorcontblack(int nro)
{

    int contadornegro = 0;

    if(nro==2|| nro==4 || nro==6 || nro==8 || nro==10 || nro==11)
    {

        contadornegro++;

    }
    else if(nro==13 || nro==15 || nro==17 || nro==20 || nro==22)
    {

        contadornegro++;

    }
    else if(nro==24 || nro==26 || nro==28 || nro==29 || nro==31 || nro==33 || nro==35)
    {

        contadornegro++;

    }
    else
    {

        contadornegro = 0;

    }

    return contadornegro;

}

//Funcion que informa las rondas que salio 0 o multiplo de 10 (Resultados 6).

int informar(int premio)
{
    int contarpremio = 0;//Cuenta las veces que salio 0 o multiplo de 10.

    if(premio == 0 || premio%10 == 0)
    {
        contarpremio++;
    }

    return contarpremio;

}


//Funcion que cuenta numeros primos (Resultados 8).

int nroprimo(int premio)
{
    int h;
    int contarprimos = 0;
    int a=0;//Usamos la variable para contar los divisiores del numero que sale sorteado

    for(h=1; h<=premio; h++)
    {

        if(premio%h == 0) //Si el modulo del premio es 0, incrementamos a en 1
            a++;
    }
    if(a==2)
    {
        contarprimos++;
    }

    return contarprimos;
}

