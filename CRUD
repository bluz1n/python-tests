import sqlite3
from datetime import datetime

conn = sqlite3.connect('crud.db')
cursor = conn.cursor()

def main():
        print ("Qual tabela gostaria de acessar? ")
        print ("Para acessar postagens, escreva POST" )
        print ("Para acessar comentarios, escreva COMMENT ")
        table = input("-> ")

        if table.lower() == "post" or table.lower() == "comment":
                crud(table)
        else:
                print("Informe um nome válido.")
        
def crud(table):
        x = input("Qual ação deseja realizar: Create(C), Read(R), Update(U) ou Delete(D)?")
        xLower = x.lower()
        if table.lower() == "post":
                if xLower == "c":
                        c_post()
                elif xLower == "r":
                        r_post()
                elif xLower == "u":
                        u_post()
                elif xLower == "d":
                        d_post()
                else:
                        print("Insira uma ação válida!!")
        else:
                if xLower == "c":
                        c_comment()
                elif xLower == "r":
                        r_comment()
                elif xLower == "u":
                        u_comment()
                elif xLower == "d":
                        d_comment()
                else:
                        print("Insira uma ação válida!!")

def c_post():
        title = input("Qual o titulo da postagem? ")
        created = datetime.now()
        text = input("Qual vai ser o conteúdo? ")
        cursor.execute("INSERT INTO post (Title, Created, Text) VALUES (?, ?, ?)", (title, created, text))
        conn.commit()
        print("Sucesso :)")


def c_comment():
        postIdAdd = input("Insira o ID da postagem ")
        textAdd = input("Qual será o comentário? ")
        created = datetime.now() 
        userAdd = input("Qual é o nome do usuario? ")
        cursor.execute("""
        SELECT PostID FROM post WHERE PostID == ?;
        """, postIdAdd)
        postId = cursor.fetchone()

        if postId == None:
                print("Algo deu errado :( ")
        
        else:
                cursor.execute("INSERT INTO comment (PostID, Text, Created, User) VALUES (?, ?, ?, ?)", (postId[0], textAdd, created, userAdd))

                conn.commit()
        
                print("Sucesso :)")

def r_post():
        cursor.execute("""
        SELECT * FROM post;
        """)

        for line in cursor.fetchall():
                print(line)


def r_comment():
        cursor.execute("""
        SELECT * FROM comment;
        """)

        for line in cursor.fetchall():
                print(line)

def u_post():
        update = input("Qual é o ID da postagem que quer alterar? ")

        cursor.execute("""
        SELECT PostID FROM post
        WHERE PostID == ?
        """, update)
        checkPost = cursor.fetchone()

        if checkPost == None:
                print("Não foi possivel encontrar esse ID ")

        else:
                data = input("Informe o que deseja alterar (titulo, texto) ")
                
                if data.lower() == "titulo":
                        newData = input("Insira o novo titulo ")

                        cursor.execute("""
                        UPDATE post SET Title = ?
                        WHERE PostID = ?
                        """, (newData, update))

                        conn.commit()

                        print("Sucesso :) ")

                elif data.lower() == "texto":
                        newData = input("Insira qual é a edição: ")

                        cursor.execute("""
                        UPDATE post SET Text = ?
                        WHERE PostID
                        """, (newData, update))

                        conn.commit()

                        print("Sucesso :) ")
                
                else:
                        print("Invalido")


def u_comment():
        update = input("Qual é o ID do comentario que quer alterar? ")

        cursor.execute("""
        SELECT CommentID FROM comment
        WHERE CommentID == ?
        """, update)
        checkComment = cursor.fetchone()

        if checkComment == None:
                print("Não foi possivel encontrar esse ID ")

        else:
                data = input("Informe o que deseja alterar (Texto, usuario) ")
                
                if data.lower() == "text":
                        newData = input("Insira o novo texto ")

                        cursor.execute("""
                        UPDATE comment SET Text = ?
                        WHERE CommentID = ?
                        """, (newData, update))

                        conn.commit()

                        print("Sucesso :) ")

                elif data.lower() == "usuario":
                        newData = input("Insira qual é o usuario: ")

                        cursor.execute("""
                        UPDATE comment SET User = ?
                        WHERE CommentID = ?
                        """, (newData, update))

                        conn.commit()

                        print("Sucesso :) ")
                
                else:
                        print("Invalido")


def d_post():
        delete = input("Qual é o ID do post a ser excluido? ")

        cursor.execute("""
        SELECT PostID from post
        WHERE PostID == ?
        """, delete)
        checkPost = cursor.fetchone()

        if checkPost == None:
                print("ID invalido ")
        else:
                cursor.execute("""
                DELETE FROM post
                WHERE PostID == ?
                """, delete)

                cursor.execute("""
                DELETE FROM comment
                WHERE PostID == ?
                """, delete)

                conn.commit()

                print("A postagem foi deletada com sucesso :)")

def d_comment():
        delete = input("Qual é o ID do comentario? ")

        cursor.execute("""
        SELECT CommentID FROM comment
        WHERE CommentID == ?
        """, delete)
        checkComment = cursor.fetchone()

        if checkComment == None:
                print("Não foi possivel encontrar esse comentario ")
        else:
                cursor.execute("""
                DELETE FROM comment
                WHERE CommentID == ?
                """, delete)

                conn.commit()

                print("Sucesso :)")

main()
