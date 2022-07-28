algoritmo Jogo_da_velha;
// Síntese
//  Objetivo: fazer um jogo da velha
//  Entrada : a posição do x ou da O
//  Saída   : o ganhador ou velha


principal
	// Declarações
	inteiro linha, coluna;
	texto N,C;
	inteiro i,j,n,g;
	inteiro prox_j, linha_i,prox_i,coluna_i,prox_c;
	real resto;
	texto matriz[3][3];
	
	// Instruções
	// regras do jogo
	regras();
	// esvaziando o jogo da velha
	para ( i de 0 ate 2 passo 1)faca
		linha = i;
		para( j de 0 ate 2 passo 1)faca
			coluna = j;
			matriz [linha][coluna] =(" ");
		fimPara
	fimPara
	// jogador escolhe a posição que quer jogar sendo que o primeiro é X e o segundo O
	g = 0;// contador de vitorias
	para( i de 1 ate 9 passo 1) faca
		se(g == 1) entao// se g for 1 algém já entrou nas condições de vencedor
			interrompa;
		senao
			N = qual_jogador(i);
			// jogador escolhe onde quer jogar
			escreval(" Jogador ",N," digite a linha :");
			leia(linha);
			escreval(" Jogador ",N," digite a coluna :");
			leia(coluna);
			// não poder repetir a mesma posição se acontecer dar erro
			se((comparaTexto (matriz[linha][coluna],"X")== 0)ou(comparaTexto (matriz[linha][coluna],"O")==0))entao// se a posição na matriz nessa posição ja tiver X ou O ela já foi
				escreval(" ");
				escreval("  Essa posição já foi");
				escreval("  insira uma nova posição: ");//e fazer com que o jogador incirra novas variáveis
				escreval("");
				N = qual_jogador(i);
				// jogador escolhe onde quer jogar
				escreval(" Jogador ",N," digite a linha :");
				leia(linha);
				escreval(" Jogador ",N," digite a coluna :");
				leia(coluna);
			fimSe
			// colocar a variavel em uma posição que está em branco ou seja não repete
			matriz[linha][coluna] = (N);
			// mostra o jogo na tela onde o jogador marcou
			escreval("          ","|","          ","|");
			escreval("    ", matriz[0][0],"     ","|","    ", matriz[0][1],"     ","|","    ",matriz[0][2],"     ");
			escreval("__________|__________|________");
			escreval("          ","|","          ","|");
			escreval("    ", matriz[1][0],"     ","|","    ", matriz[1][1],"     ","|","    ",matriz[1][2],"     ");
			escreval("__________|__________|________");
			escreval("          ","|","          ","|");
			escreval("    ", matriz[2][0],"     ","|","    ", matriz[2][1],"     ","|","    ", matriz[2][2],"     ");
			escreval("          ","|","          ","|");
			
			//comparar linha Para ver se alguém ganhou
			para ( i de 0 ate 2 passo 1)faca
				linha = i;
				prox_j = 0;
				linha_i = 0;
				para( j de 0 ate 2 passo 1)faca
					coluna = j;
					prox_j = prox_j +1;
					se(prox_j <= 2)entao
						se(comparaTexto (( matriz [linha][coluna]),(matriz [linha][prox_j]))== 0 )entao
							se(comparaTexto((matriz[linha][coluna]),(" "))!= 0) entao// não pode ser vazio
								linha_i = linha_i + 1;
								se(linha_i == 2)entao
									escreval("0 jogador ", (matriz [linha][prox_j])," ganhou na linha ",linha);
									g = g + 1; // contador
								fimSe
							fimSe
						fimSe
					fimSe
				fimPara
			fimPara
			//	comparar colunas para ver se alguém ganhou
			para ( i de 0 ate 2 passo 1)faca
				coluna = i;
				prox_j = 0;
				coluna_i = 0;
				para( j de 0 ate 2 passo 1)faca
					linha = j;
					prox_j = prox_j + 1;
					se(prox_j <= 2)entao
						se(comparaTexto (( matriz [linha][coluna]),(matriz [prox_j][coluna]))== 0 )entao
							se(comparaTexto((matriz[linha][coluna]),(" "))!= 0) entao// não pode ser vazio
								coluna_i = coluna_i + 1;
								se(coluna_i == 2)entao
									escreval("0 jogador ",(matriz [linha][coluna])," ganhou na coluna ",coluna);
									g = g+1; // contador
								fimSe
							fimSe
						fimSe
					fimSe
				fimPara
			fimPara
			// comparar diagonais descrescente
			prox_j = 0;
			prox_i = 0;
			para ( i de 0 ate 2 passo 1)faca
				coluna = i;
				linha = i;
				prox_j = prox_j + 1;
				prox_i = prox_i + 1;
				se(prox_j <= 2 e prox_i <= 2)entao
					se(comparaTexto (( matriz [linha][coluna]),(matriz [prox_j][prox_i]))== 0 )entao
						se(comparaTexto((matriz[linha][coluna]),(" "))!= 0) entao//não pode ser vazio
							coluna_i = coluna_i + 1;
							se(coluna_i == 2)entao
								escreval("0 jogador ",(matriz [linha][coluna])," ganhou na diagonal");
								g = g+1;//contador
							fimSe
						fimSe
					fimSe
				fimSe
			fimPara
			// comparar diagonais crescente
			prox_j = 3;
			prox_i = 0;
			prox_c = 2;
			coluna_i =0;
			prox_i = 0;
			para( j de 0 ate 2 passo 1)faca
				coluna = j;
				prox_i = prox_i + 1;
				prox_j = prox_j - 1;
				prox_c = prox_c - 1;
				se(((prox_j >= 0)e (prox_i <=2)e (prox_c>=0)) )entao
					se(comparaTexto (( matriz [prox_j][coluna]),(matriz [prox_c][prox_i]))== 0 )entao
						se(comparaTexto((matriz [prox_j][coluna]),(" "))!= 0) entao//não pode ser vazio
							coluna_i = coluna_i + 1;
							se(coluna_i == 2)entao
								escreval("0 jogador ",(matriz [prox_c][prox_i]),"  ganhou na diagonal");
								g=g+1;//contador
							fimSe
						fimSe
					fimSe
				fimSe
			fimPara
		fimSe
	fimPara
	// caso tenha usado todas as casas e nínguem entrou em uma condição de ganhar
	velha(g);

fimPrincipal
//regras do jogo
procedimento regras()
texto iniciar;
escreval("REGRAS: ");
	escreval("");
	escreval("O objetivo do jogo é fazer uma sequência de três símbolos iguais, seja em linha vertical, horizontal ou diagonal, enquanto tenta impedir que seu adversário faça o mesmo.");
	escreval("           ");
	escreval("LINHAS → ");
	escreval("COLUNAS ↓ ");
	escreval("          ","|","          ","|");
	escreval("     0/0  ","|","    0/1   ","|","     0/2  ");
	escreval("__________|__________|________");
	escreval("          ","|","          ","|");
	escreval("     1/0  ","|","    1/1   ","|","    1/2    ");
	escreval("__________|__________|________");
	escreval("          ","|","          ","|");
	escreval("     2/0  ","|","    2/1   ","|","    2/2    ");
	escreval("          ","|","          ","|");
	escreval("                ");
	escreval("INICIAR: ");
	escreval("  Clique no enter para começar");
	leia(iniciar);
	limpaTela();
fimProcedimento

//qual simbolo de N
funcao texto qual_jogador(inteiro i)
	inteiro resto;
	texto N;
	resto = i%2; // se não tiver resto é o jogador 2 se tiver o 1
	se( resto == 0) entao
		N = "O";
	senao
		N = "X";
	fimSe
	retorna N;
fimFuncao

procedimento velha (inteiro g)
	se(g == 0)entao
		escreval(" Deu velha ");
	fimSe
fimProcedimento	
