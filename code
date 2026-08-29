import tkinter as tk
from tkinter import messagebox
import math
import matplotlib.pyplot as plt
A = 1.0e7
Ea = 50000
R = 8.314
def calculate():
    try:
        T = float(temp_entry.get())
        V = float(volume_entry.get())
        Q = float(flow_entry.get())
        if T <= 0 or V <= 0 or Q <= 0:
            messagebox.showerror("Error", "Enter values greater than zero")
            return
        k = A * math.exp(-Ea / (R * T))
        tau = V / Q
        cstr_X = (k * tau) / (1 + k * tau)
        pfr_X = 1 - math.exp(-k * tau)
        k_result.config(text=str(round(k, 6)) + " 1/min")
        tau_result.config(text=str(round(tau, 2)) + " min")
        cstr_result.config(text=str(round(cstr_X * 100, 2)) + " %")
        pfr_result.config(text=str(round(pfr_X * 100, 2)) + " %")
        if pfr_X > cstr_X:
            better_result.config(text="PFR gives higher conversion")
        elif cstr_X > pfr_X:
            better_result.config(text="CSTR gives higher conversion")
        else:
            better_result.config(text="Both give the same conversion")
    except ValueError:
        messagebox.showerror("Error", "Please enter valid numbers")
def show_temperature_graph():
    try:
        V = float(volume_entry.get())
        Q = float(flow_entry.get())
        if V <= 0 or Q <= 0:
            messagebox.showerror("Error", "Enter valid volume and flow rate")
            return
        temperature = []
        cstr_conversion = []
        pfr_conversion = []
        tau = V / Q
        for T in range(300, 501, 10):
            k = A * math.exp(-Ea / (R * T))
            cstr_X = (k * tau) / (1 + k * tau)
            pfr_X = 1 - math.exp(-k * tau)
            temperature.append(T)
            cstr_conversion.append(cstr_X * 100)
            pfr_conversion.append(pfr_X * 100)
        plt.figure(figsize=(8, 5))
        plt.plot(temperature,cstr_conversion,marker="o",label="CSTR")
        plt.plot(temperature,pfr_conversion,marker="o",label="PFR")
        plt.xlabel("Temperature (K)")
        plt.ylabel("Conversion (%)")
        plt.title("Temperature vs Reactor Conversion")
        plt.legend()
        plt.grid()
        plt.show()
    except ValueError:
        messagebox.showerror("Error", "Enter valid volume and flow rate")
def compare_reactors():
    try:
        T = float(temp_entry.get())
        V = float(volume_entry.get())
        Q = float(flow_entry.get())
        if T <= 0 or V <= 0 or Q <= 0:
            messagebox.showerror("Error", "Enter valid values")
            return
        k = A * math.exp(-Ea / (R * T))
        tau = V / Q
        cstr_X = (k * tau) / (1 + k * tau)
        pfr_X = 1 - math.exp(-k * tau)
        reactors = ["CSTR", "PFR"]
        conversions = [cstr_X * 100,pfr_X * 100]
        plt.figure(figsize=(7, 5))
        plt.bar(reactors, conversions)
        plt.ylabel("Conversion (%)")
        plt.title("CSTR vs PFR Conversion")
        plt.grid(axis="y")
        plt.show()
    except ValueError:
        messagebox.showerror("Error", "Please enter valid values")
def optimize():
    try:
        target = float(target_entry.get())
        V = float(volume_entry.get())
        Q = float(flow_entry.get())
        if target <= 0 or target >= 100:
            messagebox.showerror("Error","Target conversion must be between 0 and 100")
            return
        if V <= 0 or Q <= 0:
            messagebox.showerror("Error","Enter valid volume and flow rate")
            return
        target = target / 100
        tau = V / Q
        found_temperature = None
        found_conversion = None
        for T in range(250, 1001):
            k = A * math.exp(-Ea / (R * T))
            cstr_X = (k * tau) / (1 + k * tau)
            if cstr_X >= target:
                found_temperature = T
                found_conversion = cstr_X * 100
                break
        if found_temperature is not None:
            optimization_result.config(text="Minimum Temperature: "+ str(found_temperature)+ " K\nExpected Conversion: "+ str(round(found_conversion, 2))+ " %")
        else:
            optimization_result.config(text="Target conversion not reached")
    except ValueError:
        messagebox.showerror("Error", "Enter valid values")
def required_volume():
    try:
        T = float(temp_entry.get())
        Q = float(flow_entry.get())
        target = float(target_entry.get())
        if T <= 0 or Q <= 0:
            messagebox.showerror("Error","Enter valid temperature and flow rate")
            return
        if target <= 0 or target >= 100:
            messagebox.showerror("Error","Target conversion must be between 0 and 100")
            return
        X = target / 100
        k = A * math.exp(-Ea / (R * T))
        tau_cstr = X / (k * (1 - X))
        volume_cstr = tau_cstr * Q
        tau_pfr = -math.log(1 - X) / k
        volume_pfr = tau_pfr * Q
        volume_result.config(text="CSTR Volume: "+ str(round(volume_cstr, 2))+ " L\n"+ "PFR Volume: "+ str(round(volume_pfr, 2))+ " L")
    except ValueError:
        messagebox.showerror("Error", "Enter valid values")
def reset():
    temp_entry.delete(0, tk.END)
    volume_entry.delete(0, tk.END)
    flow_entry.delete(0, tk.END)
    target_entry.delete(0, tk.END)
    k_result.config(text="---")
    tau_result.config(text="---")
    cstr_result.config(text="---")
    pfr_result.config(text="---")
    better_result.config(text="")
    optimization_result.config(text="---")
    volume_result.config(text="---")
window = tk.Tk()
window.title("Chemical Reactor Simulation Tool")
window.geometry("850x700")
window.resizable(False, False)
heading = tk.Label(window,text="CHEMICAL REACTOR SIMULATION TOOL",font=("Arial", 20, "bold"))
heading.pack(pady=15)
subtitle = tk.Label(window,text="CSTR and PFR Performance Analysis",font=("Arial", 11))
subtitle.pack()
main_frame = tk.Frame(window)
main_frame.pack(pady=20)
input_frame = tk.LabelFrame(main_frame,text="Reactor Inputs",font=("Arial", 11, "bold"),padx=25,pady=15)
input_frame.grid(row=0, column=0, padx=15)
tk.Label(input_frame,text="Temperature (K)").grid(row=0, column=0, pady=8)
temp_entry = tk.Entry(input_frame, width=15)
temp_entry.grid(row=0, column=1, pady=8)
tk.Label(input_frame,text="Reactor Volume (L)").grid(row=1, column=0, pady=8)
volume_entry = tk.Entry(input_frame, width=15)
volume_entry.grid(row=1, column=1, pady=8)
tk.Label(input_frame,text="Flow Rate (L/min)").grid(row=2, column=0, pady=8)
flow_entry = tk.Entry(input_frame, width=15)
flow_entry.grid(row=2, column=1, pady=8)
tk.Button(input_frame,text="CALCULATE",width=15,command=calculate).grid(row=3,column=0,columnspan=2,pady=15)
result_frame = tk.LabelFrame(main_frame,text="Simulation Results",font=("Arial", 11, "bold"),padx=25,pady=15)
result_frame.grid(row=0, column=1, padx=15)
tk.Label(result_frame,text="Rate Constant").grid(row=0, column=0, pady=7)
k_result = tk.Label(result_frame,text="---")
k_result.grid(row=0, column=1)
tk.Label(result_frame,text="Residence Time").grid(row=1, column=0, pady=7)
tau_result = tk.Label(result_frame,text="---")
tau_result.grid(row=1, column=1)
tk.Label(result_frame,text="CSTR Conversion").grid(row=2, column=0, pady=7)
cstr_result = tk.Label(result_frame,text="---")
cstr_result.grid(row=2, column=1)
tk.Label(result_frame,text="PFR Conversion").grid(row=3, column=0, pady=7)
pfr_result = tk.Label(result_frame,text="---")
pfr_result.grid(row=3, column=1)
better_result = tk.Label(result_frame,text="",font=("Arial", 10, "bold"))
better_result.grid(row=4,column=0,columnspan=2,pady=10)
graph_frame = tk.LabelFrame(window,text="Reactor Analysis",font=("Arial", 11, "bold"),padx=20,pady=15)
graph_frame.pack(pady=10)
tk.Button(graph_frame,text="TEMPERATURE vs CONVERSION",width=25,command=show_temperature_graph).grid(row=0, column=0, padx=10)
tk.Button(graph_frame,text="COMPARE CSTR vs PFR",width=25,command=compare_reactors).grid(row=0, column=1, padx=10)
optimization_frame = tk.LabelFrame(window,text="Reactor Design",font=("Arial", 11, "bold"),padx=20,pady=10)
optimization_frame.pack(pady=10)
tk.Label(optimization_frame,text="Target Conversion (%)").grid(row=0, column=0, padx=10)
target_entry = tk.Entry(optimization_frame,width=10)
target_entry.grid(row=0, column=1)
tk.Button(optimization_frame,text="FIND TEMPERATURE",command=optimize).grid(row=0, column=2, padx=10)
tk.Button(optimization_frame,text="REQUIRED VOLUME",command=required_volume).grid(row=0, column=3, padx=10)
optimization_result = tk.Label(optimization_frame,text="---")
optimization_result.grid(row=1,column=0,columnspan=4,pady=8)
volume_result = tk.Label(optimization_frame,text="---")
volume_result.grid(row=2,column=0,columnspan=4,pady=5)
tk.Button(window,text="RESET",width=15,command=reset).pack(pady=10)
window.mainloop()