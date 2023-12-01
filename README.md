# DA-in-GameDev-labwork4
Отчет по лабораторной работе #4 выполнил:
- Сабиров Глеб Анатольевич
- РИ220948


| Задание | Выполнение |
| ------ | ------ |
| Задание 1 | * |
| Задание 2 | * |
| Задание 3 | # |

## Цель работы
Изучение и реализация перцептрона с использованием Unity

## Задание 1
### в проекте Unity реализовать перцептрон, который умеет производить вычисления:
### - OR | дать комментарии о корректности работы
### - AND | дать комментарии о корректности работы
### - NAND | дать комментарии о корректности работы
### - XOR | дать комментарии о корректности работы

Скрипт перцептрона:
```cs
using System.Collections;
using System.Collections.Generic;
using UnityEngine;

[System.Serializable]
public class TrainingSet
{
	public double[] input;
	public double output;
}

public class Perceptron : MonoBehaviour {

	public TrainingSet[] ts;
	double[] weights = {0,0};
	double bias = 0;
	double totalError = 0;

	double DotProductBias(double[] v1, double[] v2) 
	{
		if (v1 == null || v2 == null)
			return -1;
	 
		if (v1.Length != v2.Length)
			return -1;
	 
		double d = 0;
		for (int x = 0; x < v1.Length; x++)
		{
			d += v1[x] * v2[x];
		}

		d += bias;
	 
		return d;
	}

	double CalcOutput(int i)
	{
		double dp = DotProductBias(weights,ts[i].input);
		if(dp > 0) return(1);
		return (0);
	}

	void InitialiseWeights()
	{
		for(int i = 0; i < weights.Length; i++)
		{
			weights[i] = Random.Range(-1.0f,1.0f);
		}
		bias = Random.Range(-1.0f,1.0f);
	}

	void UpdateWeights(int j)
	{
		double error = ts[j].output - CalcOutput(j);
		totalError += Mathf.Abs((float)error);
		for(int i = 0; i < weights.Length; i++)
		{			
			weights[i] = weights[i] + error*ts[j].input[i]; 
		}
		bias += error;
	}

	double CalcOutput(double i1, double i2)
	{
		double[] inp = new double[] {i1, i2};
		double dp = DotProductBias(weights,inp);
		if(dp > 0) return(1);
		return (0);
	}

	void Train(int epochs)
	{
		InitialiseWeights();
		
		for(int e = 0; e < epochs; e++)
		{
			totalError = 0;
			for(int t = 0; t < ts.Length; t++)
			{
				UpdateWeights(t);
				Debug.Log("W1: " + (weights[0]) + " W2: " + (weights[1]) + " B: " + bias);
			}
			Debug.Log("TOTAL ERROR: " + totalError);
		}
	}

	void Start () {
		Train(8);
		Debug.Log("Test 0 0: " + CalcOutput(0,0));
		Debug.Log("Test 0 1: " + CalcOutput(0,1));
		Debug.Log("Test 1 0: " + CalcOutput(1,0));
		Debug.Log("Test 1 1: " + CalcOutput(1,1));		
	}
	
	void Update () {
		
	}
}
```
### OR
- Перцептрон перестаёт выдавать ошибки после 3-4 эпох обучения
![image](https://github.com/nosova666/DA-in-GameDev-labwork4/blob/main/OR%20screen.png)

### AND
- Перцептрон перестаёт ошибаться в среднем после 5-6 эпох, минимально - после 3-ёх эпох
![image](https://github.com/nosova666/DA-in-GameDev-labwork4/blob/main/AND%20screen.png)

### NAND
- Перцептрон перестаёт ошибаться в среднем после 5-7 эпох обучения
![image](https://github.com/nosova666/DA-in-GameDev-labwork4/blob/main/NAND%20screen.png)

### XOR
- Перцептрон не обучается и выдаёт ошибки на всех эпохах обучения
![image](https://github.com/nosova666/DA-in-GameDev-labwork4/blob/main/XOR%20screen.png)

## Задание 2
### Построить графики зависимости количества эпох от ошибки  обучения. Указать от чего зависит необходимое количество эпох обучения.

![image](https://github.com/nosova666/DA-in-GameDev-labwork4/blob/main/diagram.png)

- Судя по всему, количество необходимых эпох для обучения зависит от степени сложности структуры логической операции, операция OR имеет простую сложность и перцептрон обучается за меньшее количество эпох обучения, AND и NAND имеют большую сложность, поэтому перцептрону в среднем требуется пройти больше эпох, чем в случае с операцией OR. Операция XOR ещё более сложная, поэтому перцептрон не может адаптироваться
и не перестаёт допускать ошибки.

## Выводы
Я научился реализовывать перцептрон с использованием Unity, построил график зависимости кол-ва эпох от ошибок обучения, сделал вывод о том, от чего зависит необходимое кол-во эпох обучения.
