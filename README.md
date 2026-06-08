# Sistema de Gestão de Barbearia

fila = []

servicos = {
    1: ["Corte", 30],
    2: ["Barba", 20],
    3: ["Corte + Barba", 45],
    4: ["Sobrancelha", 10],
    5: ["Pigmentação", 15],
    6: ["Hidratação", 25],
    7: ["Lavagem", 10]
}

clientes_atendidos = 0
servicos_realizados = 0
faturamento = 0


def mostrar_servicos():
    print("\n===== SERVIÇOS DISPONÍVEIS =====")

    for codigo in servicos:
        print(codigo, "-", servicos[codigo][0], "- R$", servicos[codigo][1])


def adicionar_cliente():
    nome = input("Nome do cliente: ").strip()

    if nome == "":
        print("Nome inválido.")
        return

    print("\nEscolha a profissional:")
    print("1 - Michele")
    print("2 - Aline")

    profissional = input("Opção: ")

    if profissional == "1":
        profissional = "Michele"
    elif profissional == "2":
        profissional = "Aline"
    else:
        print("Profissional inválida.")
        return

    lista_servicos = []

    while True:
        mostrar_servicos()

        try:
            escolha = int(input("Escolha um serviço (0 para finalizar): "))

            if escolha == 0:
                break

            if escolha in servicos:
                lista_servicos.append(escolha)
                print("Serviço adicionado!")
            else:
                print("Serviço inválido!")

        except ValueError:
            print("Digite apenas números!")

    if len(lista_servicos) == 0:
        print("Nenhum serviço foi selecionado.")
        return

    fila.append([nome, profissional, lista_servicos])

    print("Cliente adicionado à fila!")


def mostrar_fila():
    if len(fila) == 0:
        print("Fila vazia.")
    else:
        print("\n===== FILA DE CLIENTES =====")

        for i in range(len(fila)):
            print(
                i + 1,
                "-",
                fila[i][0],
                "| Profissional:",
                fila[i][1]
            )


def chamar_cliente():
    global clientes_atendidos
    global servicos_realizados
    global faturamento

    if len(fila) == 0:
        print("Não há clientes na fila.")
        return

    cliente = fila.pop(0)

    nome = cliente[0]
    profissional = cliente[1]
    lista_servicos = cliente[2]

    total = 0

    print("\n===== CLIENTE EM ATENDIMENTO =====")
    print("Nome:", nome)
    print("Profissional:", profissional)
    print("Serviços:")

    for codigo in lista_servicos:
        nome_servico = servicos[codigo][0]
        preco = servicos[codigo][1]

        print("-", nome_servico, "- R$", preco)

        total += preco
        servicos_realizados += 1

    print("Total a pagar: R$", total)

    faturamento += total
    clientes_atendidos += 1


def relatorio():
    print("\n===== RELATÓRIO DO DIA =====")
    print("Clientes atendidos:", clientes_atendidos)
    print("Serviços realizados:", servicos_realizados)
    print("Faturamento total: R$", faturamento)
    print("Clientes aguardando na fila:", len(fila))


while True:

    print("\n===== SISTEMA DE BARBEARIA =====")
    print("1 - Adicionar cliente")
    print("2 - Mostrar fila")
    print("3 - Chamar próximo cliente")
    print("4 - Relatório do dia")
    print("5 - Sair")

    opcao = input("Escolha uma opção: ")

    if opcao == "1":
        adicionar_cliente()

    elif opcao == "2":
        mostrar_fila()

    elif opcao == "3":
        chamar_cliente()

    elif opcao == "4":
        relatorio()

    elif opcao == "5":
        print("Sistema encerrado.")
        break

    else:
        print("Opção inválida!")
