import numpy as np
import matplotlib.pyplot as plt
from scipy.optimize import linprog

def resolver_simplex(c, A, b):
    print("\n🔷 Método SIMPLEX")
    resultado = linprog(c=-np.array(c), A_ub=A, b_ub=b, method='simplex')

    if resultado.success:
        print("✅ Solución encontrada:")
        print(" - Variables óptimas:", resultado.x)
        print(" - Valor óptimo de la función objetivo:", -resultado.fun)
    else:
        print("❌ No se encontró solución:", resultado.message)

    return resultado

def resolver_grafico(c, A, b):
    print("\n🔷 Método GRÁFICO (solo para 2 variables)")
    if len(c) != 2:
        print("⚠️ El método gráfico solo es posible con 2 variables.")
        return

    x_vals = np.linspace(0, max(b)*1.2, 400)
    plt.figure()

    for i, (a, bi) in enumerate(zip(A, b)):
        if a[1] != 0:
            y_vals = (bi - a[0]*x_vals) / a[1]
            plt.plot(x_vals, y_vals, label=f"Restricción {i+1}")
        else:
            x_line = bi / a[0]
            plt.axvline(x=x_line, label=f"Restricción {i+1}")

    plt.xlabel("x₁")
    plt.ylabel("x₂")
    plt.xlim(0)
    plt.ylim(0)
    plt.axhline(0, color='black', lw=0.5)
    plt.axvline(0, color='black', lw=0.5)
    plt.title("Método Gráfico")
    plt.grid(True)
    plt.legend()
    plt.show()

def analisis_sensibilidad(resultado, c, A, b):
    print("\n🔷 ANÁLISIS DE SENSIBILIDAD (básico)")

    if not resultado.success:
        print("❌ No se puede realizar el análisis porque no se obtuvo solución.")
        return

    # Precios sombra aproximados usando dualidad
    print("\n📌 Precios sombra estimados:")
    dual_vars = resultado.get("ineqlin", None)
    if hasattr(resultado, "ineqlin") and hasattr(resultado.ineqlin, "marginals"):
        precios_sombra = resultado.ineqlin.marginals
        for i, ps in enumerate(precios_sombra):
            print(f" - Restricción {i+1}: {ps:.3f}")
    else:
        print(" (No disponible con el método 'simplex' de scipy)")

    print("\n📌 Interpretación:")
    print(" - Los precios sombra muestran cuánto mejora la función objetivo si se incrementa en 1 unidad el lado derecho de cada restricción (b).")
    print(" - Si el precio sombra es 0, aumentar esa restricción no ayuda a mejorar la solución óptima.")

def interpretar_resultados(resultado, c):
    print("\n🔷 INTERPRETACIÓN DE RESULTADOS")
    if not resultado.success:
        print("❌ No se puede interpretar una solución no factible.")
        return

    for i, xi in enumerate(resultado.x):
        print(f" - Variable x{i+1} = {xi:.2f}")

    print(f"\n✅ El valor máximo de la función objetivo es: {-resultado.fun:.2f}")
    print(" - Esto significa que bajo las restricciones dadas, esta es la mejor solución posible.")

def main():
    # Puedes cambiar este ejemplo
    print("📌 Resolviendo: Max Z = 3x₁ + 5x₂")
    print("s.a.:")
    print(" - x₁ + 2x₂ ≤ 10")
    print(" - 3x₁ + x₂ ≤ 15")
    print(" - x₁, x₂ ≥ 0")

    c = [3, 5]  # Coeficientes de la función objetivo
    A = [
        [1, 2],
        [3, 1]
    ]
    b = [10, 15]

    resultado = resolver_simplex(c, A, b)
    resolver_grafico(c, A, b)
    analisis_sensibilidad(resultado, c, A, b)
    interpretar_resultados(resultado, c)

if __name__ == "__main__":
    main()
