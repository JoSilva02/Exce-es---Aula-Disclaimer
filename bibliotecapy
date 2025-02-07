class LivroIndisponivelError(Exception):
    def __init__(self, titulo_livro, motivo):
        self.titulo_livro = titulo_livro
        self.motivo = motivo
        super().__init__(f'O livro "{titulo_livro}" está indisponível por {motivo}')
    
class DevoluçãoInvalidaError(Exception):
    def __init__(self, usuario, livro):
        self.usuario = usuario
        self.livro = livro
        super().__init__(f'O livro "{livro}" não pode ser devolvido, pois não foi ele que pegou emprestado.')

class EmprestimoAtrasadoError(Exception):
    def __init__(self, usuario, livro, dias_atraso):
        self.usuario = usuario
        self.livro = livro
        self.dias_atraso = dias_atraso
        self.multa = dias_atraso * 2.50
        super().__init__(f'Usuário {usuario} atrasou a devolução de "{livro}" em {dias_atraso} dias. Aplicando Multa de {self.multa:.2f} reais.')

class Biblioteca:
    def __init__(self):
        self.livros_disp = {}
        self.livros_empres = {}
        self.reservas = {}

    def lend_book(self, titulo_livro, usuario):
        try:
            if not isinstance(titulo_livro, str):
                raise TypeError('O título do livro deve ser uma string')
            if titulo_livro not in self.livros_disp:
                raise LivroIndisponivelError(titulo_livro, "livro não disponivel")
            if self.livros_disp[titulo_livro] == 0:
                raise LivroIndisponivelError(titulo_livro, "já está emprestado ou reservado.")
            
            self.livros_disp[titulo_livro] -= 1
            self.livros_empres[titulo_livro] = usuario
            print(f'Livro "{titulo_livro}" emprestado para {usuario}.')
        except LivroIndisponivelError as e:
            print(e)
        except TypeError as e:
            print(e)
        except Exception as e:
            print("Error Inesperado! Favor contatar o administrador da biblioteca.")

    def getback_book(self, titulo_livro, usuario, dias_atraso):
        try:
            if titulo_livro not in self.livros_empres or self.livros_empres[titulo_livro] != usuario:
                raise DevoluçãoInvalidaError(usuario, titulo_livro)
            self.livros_disp[titulo_livro] += 1
            del self.livros_empres[titulo_livro]

            if dias_atraso > 0:
                raise EmprestimoAtrasadoError(usuario, titulo_livro, dias_atraso)
            
            print(f'Livro "{titulo_livro}" devolvido por {usuario}.')

        except DevoluçãoInvalidaError as e:
            print(e)
        except EmprestimoAtrasadoError as e:
            print(e)
        except Exception as e:
            print("Error Inesperado! Favor contatar o administrador da biblioteca")

    def reserv_book(self, titulo_livro, usuario):
        try:
            if titulo_livro not in self. livros_disp:
                raise LivroIndisponivelError(titulo_livro, "livro não disponivel.")
            if titulo_livro in self.reservas:
                raise LivroIndisponivelError(titulo_livro, "livro já está reservado.")

            self.reservas[titulo_livro] = usuario
            print(f'Livro "{titulo_livro}" reservado para {usuario}')

        except DevoluçãoInvalidaError as e:
            print(e)
        except Exception as e:
            print("Error Inesperado! Favor contatar o administrador da biblioteca")

# TESTE

biblioteca = Biblioteca()
biblioteca.livros_disp = {
    "Python para Iniciantes": 1,
    "Python Avançado": 1,
    "Machine Learning Básico": 1
}

biblioteca.lend_book("Python para Iniciantes", "João")
biblioteca.lend_book("Python para Iniciantes", "Maria")

biblioteca.getback_book("Python Avançado", "Maria", 4)

biblioteca.reserv_book("Machine Learning Básico", "João")
biblioteca.reserv_book("Machine Learning Básico", "Maria")

biblioteca.lend_book(123, "João")

biblioteca.lend_book("Python Avançado", "João")
biblioteca.getback_book("Python Avançado", "João", 5)
