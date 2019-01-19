#include <stdio.h>
#include <string.h>
#include <stdlib.h>
int main()
{
	FILE *fs = fopen("1.txt", "r");
	FILE *fa = fopen("2.txt", "w");
	int Step,End,Point;
	char Buffer[200],Value[200];
	/*两次读数为一次循环*/ 
		while (!feof(fs))
	{
		fscanf(fs, "%s", Buffer);//读取源文本的字符串到Buffer数组中 
		Point = Step = strchr(Buffer,'|') - Buffer;//在buffer中找出'|'第一次出现的位置，并返回出现指针的位置 
		Point++;;//表示Value的长度
		strncpy(Value, Buffer, Step);//将Buffer中的Step个字符复制给Value 
		Value[Step] = ' '; //同一行两字段用空格分开 
		for (int i = 0; i < 3; i++)
			Step = strchr(Buffer + Step + 1, '|') - Buffer; // 再次位移3个'|' 得到第4个 '|' 的位置
		Step += 1; //跳过'|' 字符
		End = strchr(Buffer + Step, '|') - Buffer;  //获得第5个'|' 位置
		End = End - Step;  //获得第4到第五个'|'的长度
		strncpy(Value+Point, Buffer+Step, End);//将Buffer+Step中的End个字符拷贝给Value+Point 
		Point += End; //获得长度 
		Value[Point] = '\0'; //设置结束符
		fprintf(fa, "%s\n", Value);
	}
	fclose(fs);
	fclose(fa);
	return 0;
}
