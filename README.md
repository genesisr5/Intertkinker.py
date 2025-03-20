import tkinter as tk
from tkinter import ttk, messagebox
from tkcalendar import DateEntry

def agregar_evento():
    fecha = date_entry.get()
    hora = hora_entry.get()
    descripcion = descripcion_entry.get()
    if fecha and hora and descripcion:
        tree.insert("", "end", values=(fecha, hora, descripcion))
        limpiar_campos()
    else:
        messagebox.showwarning("Advertencia", "Todos los campos son obligatorios.")

def eliminar_evento():
    seleccionado = tree.selection()
    if seleccionado:
        tree.delete(seleccionado)
    else:
        messagebox.showwarning("Advertencia", "Seleccione un evento para eliminar.")

def limpiar_campos():
    date_entry.set_date("")
    hora_entry.delete(0, tk.END)
    descripcion_entry.delete(0, tk.END)

# Configuración de la ventana principal
root = tk.Tk()
root.title("Gestor de Eventos")
root.geometry("500x400")

# Frame para la lista de eventos
tree_frame = tk.Frame(root)
tree_frame.pack(pady=10)

columns = ("Fecha", "Hora", "Descripción")
tree = ttk.Treeview(tree_frame, columns=columns, show="headings")
for col in columns:
    tree.heading(col, text=col)
    tree.column(col, width=150)
tree.pack()

# Frame para entrada de datos
input_frame = tk.Frame(root)
input_frame.pack(pady=10)

tk.Label(input_frame, text="Fecha:").grid(row=0, column=0, padx=5, pady=5)
date_entry = DateEntry(input_frame, width=12, background='darkblue', foreground='white', borderwidth=2)
date_entry.grid(row=0, column=1, padx=5, pady=5)

tk.Label(input_frame, text="Hora:").grid(row=1, column=0, padx=5, pady=5)
hora_entry = tk.Entry(input_frame)
hora_entry.grid(row=1, column=1, padx=5, pady=5)

tk.Label(input_frame, text="Descripción:").grid(row=2, column=0, padx=5, pady=5)
descripcion_entry = tk.Entry(input_frame)
descripcion_entry.grid(row=2, column=1, padx=5, pady=5)

# Frame para botones
button_frame = tk.Frame(root)
button_frame.pack(pady=10)

tk.Button(button_frame, text="Agregar Evento", command=agregar_evento).grid(row=0, column=0, padx=5)
tk.Button(button_frame, text="Eliminar Evento", command=eliminar_evento).grid(row=0, column=1, padx=5)
tk.Button(button_frame, text="Salir", command=root.quit).grid(row=0, column=2, padx=5)

root.mainloop()
