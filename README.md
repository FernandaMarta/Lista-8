import java.util.ArrayList;
import java.util.Scanner;

class Empregado {
    private String nome;
    private int idade;
    private double salario;

    public Empregado(String nome, int idade, double salario) {
        this.nome = nome;
        this.idade = idade;
        this.salario = salario;
    }

    public String getNome() {
        return nome;
    }

    public void setNome(String nome) {
        this.nome = nome;
    }

    public int getIdade() {
        return idade;
    }

    public void setIdade(int idade) {
        this.idade = idade;
    }

    public double getSalario() {
        return salario;
    }

    public void setSalario(double salario) {
        this.salario = salario;
    }


    public String toString() {
        return "Nome: " + nome + ", Idade: " + idade + ", Salário: R$" + salario;
    }

    public void promover() {
        if (idade > 18) {
            double aumento = salario * 0.25;
            aumentarSalario(aumento);
            System.out.println("Promoção realizada com sucesso!");
        } else {
            System.out.println("O empregado não atende aos requisitos para a promoção.");
        }
    }

    public void aumentarSalario(double percentual) {
        salario += salario * percentual;
    }

    public void demitir(int motivo) {
        switch (motivo) {
            case 1: // Justa causa
                System.out.println("O empregado foi demitido por justa causa.");
                // Realizar aviso prévio, se necessário
                break;
            case 2: // Decisão do empregador
                double multa = salario * 0.4;
                salario -= multa;
                System.out.println("O empregado foi demitido por decisão do empregador.\nMulta aplicada: R$" + multa);
                break;
            case 3: // Aposentadoria
                double salarioAposentadoria = calcularSalarioAposentadoria();
                salario = salarioAposentadoria;
                System.out.println("O empregado foi aposentado.\nSalário de aposentadoria: R$" + salarioAposentadoria);
                break;
            default:
                System.out.println("Motivo de demissão inválido.");
        }
    }

    public void fazerAniversario() {
        idade++;
        System.out.println("Feliz aniversário! O empregado agora tem " + idade + " anos.");
    }

    private double calcularSalarioAposentadoria() {
        if (salario >= 1000 && salario < 2000) {
            return 1500;
        } else if (salario >= 2000 && salario < 3000) {
            return 2500;
        } else if (salario >= 3000 && salario < 4000) {
            return 3500;
        } else {
            return 4000;
        }
    }
}

public class Principal {
    public static void main(String[] args) {
        Scanner scanner = new Scanner(System.in);
        ArrayList<Empregado> listaEmpregados = new ArrayList<>();

        int opcao;
        do {
            System.out.println("\n=== Menu ===");
            System.out.println("1. Criar novo empregado");
            System.out.println("2. Promover empregado");
            System.out.println("3. Aumentar salário do empregado");
            System.out.println("4. Demitir empregado");
            System.out.println("5. Fazer aniversário do empregado");
            System.out.println("6. Mostrar detalhes dos empregados");
            System.out.println("7. Sair");
            System.out.print("Escolha uma opção: ");
            opcao = scanner.nextInt();

            switch (opcao) {
                case 1:
                    criarNovoEmpregado(scanner, listaEmpregados);
                    break;
                case 2:
                    promoverEmpregado(scanner, listaEmpregados);
                    break;
                case 3:
                    aumentarSalarioEmpregado(scanner, listaEmpregados);
                    break;
                case 4:
                    demitirEmpregado(scanner, listaEmpregados);
                    break;
                case 5:
                    fazerAniversarioEmpregado(scanner, listaEmpregados);
                    break;
                case 6:
                    mostrarDetalhesEmpregados(listaEmpregados);
                    break;
                case 7:
                    System.out.println("Saindo do programa...");
                    break;
                default:
                    System.out.println("Opção inválida. Tente novamente.");
            }
        } while (opcao != 7);
        
        scanner.close();
    }

    public static void criarNovoEmpregado(Scanner scanner, ArrayList<Empregado> listaEmpregados) {
        System.out.print("Nome do empregado: ");
        String nome = scanner.next();
        System.out.print("Idade do empregado: ");
        int idade = scanner.nextInt();
        System.out.print("Salário do empregado: ");
        double salario = scanner.nextDouble();

        Empregado empregado = new Empregado(nome, idade, salario);
        listaEmpregados.add(empregado);
        System.out.println("Empregado criado com sucesso.");
    }

    public static void promoverEmpregado(Scanner scanner, ArrayList<Empregado> listaEmpregados) {
        System.out.print("Índice do empregado a ser promovido: ");
        int indice = scanner.nextInt();
        Empregado empregado = listaEmpregados.get(indice);

        empregado.promover();
    }

    public static void aumentarSalarioEmpregado(Scanner scanner, ArrayList<Empregado> listaEmpregados) {
        System.out.print("Índice do empregado a ter o salário aumentado: ");
        int indice = scanner.nextInt();
        Empregado empregado = listaEmpregados.get(indice);

        System.out.print("Percentual de aumento (em decimal): ");
        double percentual = scanner.nextDouble();

        empregado.aumentarSalario(percentual);
        System.out.println("Salário aumentado com sucesso.");
    }

    public static void demitirEmpregado(Scanner scanner, ArrayList<Empregado> listaEmpregados) {
        System.out.print("Índice do empregado a ser demitido: ");
        int indice = scanner.nextInt();
        Empregado empregado = listaEmpregados.get(indice);

        System.out.println("Motivos de demissão:\n1. Justa causa\n2. Decisão do empregador\n3. Aposentadoria");
        System.out.print("Informe o motivo: ");
        int motivo = scanner.nextInt();

        empregado.demitir(motivo);
        listaEmpregados.remove(indice);
        System.out.println("Empregado demitido com sucesso.");
    }

    public static void fazerAniversarioEmpregado(Scanner scanner, ArrayList<Empregado> listaEmpregados) {
        System.out.print("Índice do empregado a fazer aniversário: ");
        int indice = scanner.nextInt();
        Empregado empregado = listaEmpregados.get(indice);

        empregado.fazerAniversario();
    }

    public static void mostrarDetalhesEmpregados(ArrayList<Empregado> listaEmpregados) {
        if (listaEmpregados.isEmpty()) {
            System.out.println("Não há empregados cadastrados.");
        } else {
            System.out.println("Detalhes dos empregados:");
            for (int i = 0; i < listaEmpregados.size(); i++) {
                System.out.println("Índice " + i + ": " + listaEmpregados.get(i));
            }
        }
    }
}
