# All-sort-ways-with-linked-lists-by-me
//my small project with C langage 


/////////////////////////////////////////////////////////// BY RAYANE BOUCHAIR //////////////////////////////////////////////////////////////////////////////


#include <stdio.h>
#include <stdlib.h>
#include <string.h>

typedef struct {
  int val;
  struct element *suiv;

} element;
typedef element *liste;


void InsererDEBUT(liste *L, int n) {
  liste p;
  p = (liste)malloc(sizeof(element));
  p->val = n;
  if (*L == NULL) {
    *L = p;
    (*L)->suiv = NULL;
  } else {
    p->suiv = *L;
    *L = p;
  }
}

void InsererFin(liste *L, int nbr) {
  liste p;
  liste courant;
  p = (liste)malloc(sizeof(element));
  p->val=nbr;
  p->suiv=NULL;

  if (*L == NULL) {
    (*L) = p;
   } else {
           courant = *L;
            while (courant->suiv != NULL) {
             courant = courant->suiv;
            }
             courant->suiv = p;
      
    
    }
}


liste CreerListe(int nbr) {

  char reponse;
  liste L;
  L = NULL;
  int valleur;

do{
  printf("\n\n  POUR Inserer au \20DEBUT\21 Ecrire 'd' ,sinon a la \20FIN\21 Ecrire 'f' \n");
  reponse = getche();
}while (reponse!='f' && reponse!='F' && reponse!='d' && reponse!='D');

switch (reponse)
{
case 'd':
case 'D':

    for (int j = 1; j <= nbr; j++) {
      printf("\nELEMENT(%d)==", j);
      scanf("%d", &valleur);
      InsererDEBUT(&L, valleur);
    }
  break;

case 'f':
case 'F':
  
   for (int t = 1; t <= nbr; t++) {
      printf("\nELEMENT(%d)==", t);
      scanf("%d", &valleur);
      InsererFin(&L, valleur);

    }
   break;


}
  return L;

}




liste Fusionner (liste L1,liste L2)
{
liste Lf;
Lf=NULL;


  if (L1==NULL ) {return L2; /* lkanat  la liste 1 mknch */
   //{ 
    //while (L2!=NULL)
   //{
     // InsererFin(&Lf,L2->val);
       //L2=L2->suiv;
   //}
    //}
  }else if (L2==NULL)   {return L1;}        /* lkanat ha la liste 2 eme mknch ya3ni null */
   //{ 
     // while (L1!=NULL)
      //{
       //InsererFin(&Lf,L1->val);
        //L1=L1->suiv;
      //}
    // } 
   else { 
 

  
     
   while (L1!=NULL && L2!=NULL)
   {
      
     if ( L1->val <= L2->val )  
      {
       InsererFin(&Lf,L1->val);  /* hna dirt b inserfin bech l3onsor li dakhalto lawal nel9ah f lawal be3da w tji l7ala mstikiya bien ya chriki ya lhaycha  */
        L1=L1->suiv;       /* lazem nroh l l'element f la liste li morah */

      }else            //if ( (L1->val > L2->val) || (L1==NULL) )  hadi nehtajha hta nverifier chart lfok +_+
        {
         InsererFin(&Lf,L2->val);
          L2=L2->suiv;     /* kifkif nmchi b7a l'element ta3 la liste li hazit mnha di sghir */
        }
      
   }
      if (L1==NULL)
      {
         while (L2!=NULL)
        {
         InsererFin(&Lf,L2->val);
          L2=L2->suiv;
        }
     }else 
     {
        while (L1!=NULL)
       {
         InsererFin(&Lf,L1->val);
          L1=L1->suiv;
       }
     }
  
   return Lf;
   }
}


void TriParSelection (liste *L)
{
 liste c,cm,min;
 int copy;

c=*L;

 while (c!=NULL)
 {
    
     min = c;
      cm=c->suiv;                //cm:courant 'marche'

      while (cm!=NULL)
      {
         if (min->val > cm->val)
          { min=cm; }     /*on rechercher la petite valleur dans la partie non trie*/
        cm=cm->suiv; 
      }
        copy = min->val;
         min->val = c->val;   /*on fait un permutation entre le min et le premier courant*/
          c->val = copy;
    

  c=c->suiv;
 }
}



void TriParFusion (liste *L)
{
 liste demiliste1,demiliste2 ,liste;
    int taille;
    taille = 0;
   liste = *L;
     while (liste!= NULL)
     {
       taille++;
        liste=liste->suiv;
     }

    if (taille> 1)
    {
        demiliste1= NULL;
        demiliste2 = NULL;

        liste = *L;

        for (int i=1; i<= taille / 2; i++)
        {
            InsererFin(&demiliste1, liste->val);
            liste = liste->suiv;
        }
        
        while (liste != NULL)   // on continuer ta3mar ta3 demi liste 2 eme mnyn hbsna be3da 
        {
            InsererFin(&demiliste2, liste->val);
            liste = liste->suiv;
        }

        TriParFusion(&demiliste1);
        TriParFusion(&demiliste2);

        *L = Fusionner(demiliste1, demiliste2);
    }
}





void affichierliste(liste L) {
  liste p;
  p = L;
  printf("\n \t\t\20\20\20\20\20\20LES VALLEUR DE LA LISTE EST :\21\21\21\21\21\21\n");
  while (p != NULL) {
    printf("|\20 %d", p->val);
    p = p->suiv;
  }
}

int menu (){
  int choix;

    printf("*\n\t\t\t\20\20\20\20\20\20 LE MENU DISPONIBLE : \21\21\21\21\21\21\n"); 
   printf("*\t\20\20 1-Trie Votre Liste avec la methode  'TRI_PAR_FUSIONNE' \t*\n");  
   printf("*\t\20\20 2-Trie Votre Liste avec la methode  'TRI_PAR_SELECTION' \t*\n"); 
    printf("*\t\20\20 3-Ajouter un element un autre fois  \t*\n"); 
   printf("*\t\20\20 4-EXIT \t*\n"); 
 printf("*\t\20");  scanf ("%d",&choix);
  return choix;
}

int main() {
  liste l;
  int nbr1,choix,choixfinal,valeur,choixinserer;

  printf ("\n\n \t\t\20\20\20\20PROGRAM DE LES METHODE DE TRIATION DES LISTES\21\21\21\21\n\n");
  printf ("Cliquez pour demarer le program .......\n");
  system ("pause");
 
  do {
      printf("\n\t\20\3BONSOIR \3 DONNER NOMBRE DES ELEMENTS DE VOTRE LISTE LINEARE :\n\20");
       scanf("%d",&nbr1);
      }while (nbr1<0);
l=CreerListe(nbr1);
do {
do {
    choix=menu();
    switch (choix){
      case 1:
        TriParFusion(&l);
        affichierliste(l);
        break;
      case 2:
        TriParSelection(&l);
        affichierliste(l);
        break;
        case 3:
        printf("\n Donner l'element pour ajouter a la liste \n");
        scanf("%d",&valeur);
        printf("\nvous voulez inserer AU [debut =1 ou FIN =2]\n");
        scanf("%d",&choixinserer);
        do {
        switch (choixinserer)
        {
        case 1: 
        InsererDEBUT(&l,valeur);
          break;
        case 2:
        InsererFin(&l,valeur);
          break;
        }
        }while (choixinserer !=1 && choixinserer !=2);

        printf("\n Le nouveau Liste est : \n\n");
        affichierliste(l);
        case 4: 
        break;

        default: printf("\t\t[MESSAGE]:!!!!!!!??????????? ERREUR CHOIX.......\n");
    }
}while (choix != 1 && choix !=2 && choix !=3 && choix!=4);

printf("\n\n Pour repeter le menu ecrire [1],sinon ecrire [0]\n");
scanf("%d",&choixfinal);

}while (choixfinal!=0);


printf("\n ************************************************************\3\3AU REVOIR\3\3***********************************************************");
 

  return 0;
}
