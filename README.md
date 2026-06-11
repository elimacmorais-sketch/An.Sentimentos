"""
ANALISADOR DE SENTIMENTOS - PROJETO EDUCACIONAL
Programa que analisa se uma frase é positiva, negativa ou neutra
Autor: Turma de Engenharia de Software
"""

# ______________________________________________________________________________
# PARTE 1: CRIANDO O DICIONÁRIO DE PALAVRAS
# ______________________________________________________________________________
# Um dicionário em Python usa chaves {} e armazena pares de chave:valor

# Lista de palavras POSITIVAS
palavras_positivas = [
    "feliz", "alegre", "ótimo", "excelente", "maravilhoso", "bom", "amor",
    "adorar", "incrível", "fantástico", "perfeito", "legal", "bacana",
    "sucesso", "vitória", "paz", "amizade", "sorrir", "esperança", "lindo",
    "bonito", "agradável", "divertido", "animado", "satisfeito", "grato"
]

# Lista de palavras NEGATIVAS
palavras_negativas = [
    "triste", "ruim", "péssimo", "horrível", "terrível", "ódio", "odiar",
    "chorar", "fracasso", "derrota", "medo", "raiva", "feio", "chato",
    "desagradável", "entediado", "frustrado", "decepcionado", "cansado",
    "preocupado", "ansioso", "difícil", "problema", "mal", "infeliz"
]


# ______________________________________________________________________________
# PARTE 2: FUNÇÃO PARA LIMPAR E PREPARAR O TEXTO
# ______________________________________________________________________________
# Esta função remove pontuações e converte tudo para minúsculas
# Exemplo: "Olá, Mundo!" vira "olá mundo"

def limpar_texto(texto):

    # Lista de pontuações que queremos remover
    pontuacoes = ".,!?;:()-\"'…"

    # Converter todo o texto para minúsculas
    texto_limpo = texto.lower()

    # Remover cada pontuação, uma por uma
    for pontuacao in pontuacoes:
        texto_limpo = texto_limpo.replace(pontuacao, "")

    return texto_limpo


# ______________________________________________________________________________
# PARTE 3: FUNÇÃO PRINCIPAL DE ANÁLISE
# ______________________________________________________________________________
# Analisa o sentimento de uma frase comparando com nosso dicionário
# Retorna: número de positivas, negativas e lista de palavras encontradas

def analisar_sentimento(frase):

    # Limpar o texto (remover pontuação e deixar em minúsculas)
    frase_limpa = limpar_texto(frase)

    # Separar a frase em palavras individuais
    palavras = frase_limpa.split()

    # Contadores: começam em zero
    contador_positivas = 0
    contador_negativas = 0

    # Listas para guardar as palavras que encontramos
    positivas_encontradas = []
    negativas_encontradas = []

    # Analisar cada palavra da frase
    for palavra in palavras:
        # Verificar se a palavra está na lista de positivas
        if palavra in palavras_positivas:
            contador_positivas += 1  # Aumenta o contador
            positivas_encontradas.append(palavra)  # Adiciona na lista

        # Verificar se a palavra está na lista de negativas
        elif palavra in palavras_negativas:
            contador_negativas += 1
            negativas_encontradas.append(palavra)

    # Retornar os resultados
    return contador_positivas, contador_negativas, positivas_encontradas, negativas_encontradas


# ______________________________________________________________________________
# PARTE 4: FUNÇÃO PARA ADICIONAR NOVAS PALAVRAS
# ______________________________________________________________________________
# Permite que o usuário adicione novas palavras ao dicionário

def adicionar_palavra():

    print("\n" + "_"*50)
    print("ADICIONAR NOVA PALAVRA AO DICIONÁRIO")

    nova_palavra = input("Digite a palavra que deseja adicionar: ").lower().strip()

    # Verificar se a palavra já existe
    if nova_palavra in palavras_positivas:
        print(f"👍  A palavra '{nova_palavra}' já está no dicionário de POSITIVAS!")
        return
    elif nova_palavra in palavras_negativas:
        print(f"👎  A palavra '{nova_palavra}' já está no dicionário de NEGATIVAS!")
        return

    # Perguntar se é positiva ou negativa
    print("\nEsta palavra é:")
    print("1️⃣ Positiva")
    print("2️⃣ Negativa")

    escolha = input("Digite sua escolha (1 ou 2): ")

    if escolha == "1":
        palavras_positivas.append(nova_palavra)
        print(f"👍 Palavra '{nova_palavra}' adicionada às POSITIVAS!")
    elif escolha == "2":
        palavras_negativas.append(nova_palavra)
        print(f"👎 Palavra '{nova_palavra}' adicionada às NEGATIVAS!")
    else:
        print("⚠️ Opção inválida! Palavra não adicionada.")


# ______________________________________________________________________________
# PARTE 5: FUNÇÃO PARA EXIBIR OS RESULTADOS
# ______________________________________________________________________________
# Mostra os resultados da análise de forma organizada

def exibir_resultados(frase, pos_count, neg_count, pos_list, neg_list):

    print("\n" + "_"*50)
    print("RESULTADO DA ANÁLISE")
    print(f"Frase analisada: \"{frase}\"")

    # Mostrar contadores
    print(f"📉 Palavras positivas encontradas: {pos_count}")
    print(f"📈 Palavras negativas encontradas: {neg_count}")

    # Mostrar as palavras identificadas
    if pos_list:
        print(f"👍 Positivas: {', '.join(pos_list)}")

    if neg_list:
        print(f"👎 Negativas: {', '.join(neg_list)}")

    # Determinar o sentimento geral
    print("-"*50)

    if pos_count > neg_count:
        print("😊 SENTIMENTO: POSITIVO")
    elif neg_count > pos_count:
        print("😞 SENTIMENTO: NEGATIVO")
    else:
        print("😐 SENTIMENTO: NEUTRO")



# ______________________________________________________________________________
# PARTE 6: PROGRAMA PRINCIPAL (MENU)
# ______________________________________________________________________________
# Função principal que controla o fluxo do programa

def main():

    print("ANALISADOR DE SENTIMENTOS ❤️")

    # Loop infinito - o programa só para quando o usuário escolher sair
    while True:
        print("\n" + "_"*50)
        print("MENU PRINCIPAL")
        print("1️⃣ Analisar uma frase")
        print("2️⃣ Adicionar palavra ao dicionário")
        print("3️⃣ Ver estatísticas do dicionário")
        print("4️⃣ Sair do programa")

        opcao = input("Escolha uma opção (1-4): ")

        # OPÇÃO 1: Analisar frase
        if opcao == "1":
            frase_usuario = input("\nDigite a frase para análise: ")

            # Verificar se o usuário digitou algo
            if frase_usuario.strip() == "":
                print("⚠️ Você não digitou nenhuma frase!")
                continue

            # Chamar a função de análise
            pos, neg, pos_palavras, neg_palavras = analisar_sentimento(frase_usuario)

            # Mostrar os resultados
            exibir_resultados(frase_usuario, pos, neg, pos_palavras, neg_palavras)

        # OPÇÃO 2: Adicionar palavra
        elif opcao == "2":
            adicionar_palavra()

        # OPÇÃO 3: Estatísticas
        elif opcao == "3":
            print("\n" + "_"*50)
            print("ESTATÍSTICAS DO DICIONÁRIO")
            print(f"Total de palavras positivas: {len(palavras_positivas)}")
            print(f"Total de palavras negativas: {len(palavras_negativas)}")
            print(f"Total geral: {len(palavras_positivas) + len(palavras_negativas)}")

        # OPÇÃO 4: Sair
        elif opcao == "4":
            print("\n👋 Obrigado por usar o Analisador de Sentimentos!")
            break  # Sai do loop e encerra o programa

        # Opção inválida
        else:
            print("\n⚠️ Opção inválida! Por favor, escolha entre 1 e 4.")


# ==============================================================================
# EXECUTAR O PROGRAMA
# ==============================================================================
# Esta linha verifica se o arquivo está sendo executado diretamente

if __name__ == "__main__":
    main()