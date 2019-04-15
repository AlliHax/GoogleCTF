## Floppy 1

You are given a foo.ico file that seems a little fishy. Let's take a look.

What happens when you read it in the terminal?


```
cat foo.ico
```

Here is the output:

```
   �( @����������������������������DDDA������DDDC333333���O��K������1OOOO�������G��K�������1����DDDI����������G��K������1ODOI�������G��K�������1��DDDI��	�	��O��K�
      �3����1OODI�0��3�����G��K��
                                 ������1DDDI��0��	��1O��K���
                                                                  �0���1DDOI���0��0����1DDGK���
               ����1G��H�
                         �0����1OODI���

                                       �1G��@	
                                                ��00��1DDDI����
                                                               𙐘1O��I����0�	1D�DI���	��
          ��1DOtI�	��1O��I������1DDDI    1O��A��������1ODO�	1G��A����������1DDDI1DDDK�����������������]?P���L��>{�
driver.txtUT	�-[�-[ux
                        O�S_�A
�0�9�;�Wҭ
E���a6��vp�i Xq	:��ٻ����'-�h!�:��b�&g�R�qh����M�n���z�}�:	܁<IO��+H(�T�����L慄f��www.comUT	�-[�-[ux
                        O�S_=��N�0�w��TP�wɆ��Ⲯq���t#\,-8[�L�S�]�<�G���{�\�����Uka9�XX�%wv%K�l1	h����k���%U!�G^�6Uq;��zw�_����g94�{�ٽ����=v±[�����m�9^}�|c	=)RxO��2Sgm������E�g2�c�1U��z�)�>��+�FKQ"�������ʑ?J�ѿ�A�P���L��>{�
��driver.txtUT�-[ux
                   O�S_P��L慄f�����www.comUT�-[ux
                                                 O�S_PK�
```

Hmm, it seems to be all gibberish. Although there are two lines that stand out to me.

```
��driver.txtUT�-[ux
```

and

```
O�S_P��L慄f�����www.comUT�-[ux
```

Now why would an .ico file have other files in it? Let's try to extract them.

```
unzip foo.ico
```
The result:

```
Archive:  foo.ico
warning [foo.ico]:  765 extra bytes at beginning or within zipfile
  (attempting to process anyway)
  inflating: driver.txt              
  inflating: www.com            
```

Well, that went well!
Let's check out this .txt file.

```
cat driver.txt
```

The result:
  
```
  This is the driver for the Aluminum-Key Hardware password storage device.
     CTF{qeY80sU6Ktko8BJW}
```

Success, on to the next challenge!
