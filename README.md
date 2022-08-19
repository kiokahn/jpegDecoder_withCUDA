# JPEG Decoder with CUDA

original : https://github.com/NVIDIA/CUDALibrarySamples/blob/master/nvJPEG/nvJPEG-Decoder/README.md

Tested :  MS WIndows 10 Pro, x64, Viual studio 2022(v143), Windows SDK 10.0.19041.0

Modified By Kiok Ahn (kiokahn@gazzi.ai, kiokahn76@gmail.com)

# Test

Reference : decode.bat
Example : 
```
nvjpegDecoder.exe -i G:\source\CUDALibrarySamples\nvJPEG\nvJPEG-Decoder_build\Debug\img\ -o G:\source\CUDALibrarySamples\nvJPEG\nvJPEG-Decoder_build\Debug\out\ -fmt rgb
```

# Requerment


[ Visual Studio Community](https://visualstudio.microsoft.com/ko/vs/community/)
Windows SDK 10.0.xxxxx
[NVIDIA GPU Computing Toolkit v11.7](https://developer.nvidia.com/cuda-downloads?target_os=Windows&target_arch=x86_64&target_version=11&target_type=exe_local)


# Key Functions

### nvjpegDecoder.cpp

- �ֿ� �Լ�  : process_images(...)
double process_images(FileNames &image_names, decode_params_t &params, double &total)
```
��� : �̹��� ���ڵ� �ֿ� ó�� �Լ�
�Է� ������ : FileNames &image_names
             �ǹ� : ���ڵ��� JPEG ���� ����� ���, ����
�Է� ������ : decode_params_t &params
             �ǹ� : GPU ���ڵ� ��� ����
```

- �ֿ� �Լ�  : decode_images(...)
int decode_images(const FileData &img_data, const std::vector<size_t> &img_len, std::vector<nvjpegImage_t> &out, decode_params_t &params, double &time) 
```
��� : GPU�� �̿��� ������ ���ڵ�
�Էµ����� : const FileData &img_data
             ���� : typedef std::vector<std::vector<char> > FileData;
             �ǹ� : JPEG ���ڵ��� �� ������ ���۵��� ����, 
��� ������ : std::vector<nvjpegImage_t> &out
             �ǹ� : ���ڵ��� �� ������ ���۵��� ����, 
                    RGB, YUV���� ������ ������ "decode_params_t &params" �� ���� ���� ��
```

- �ֿ� �Լ�  : write_images(...)
int write_images(std::vector<nvjpegImage_t> &iout, std::vector<int> &widths, std::vector<int> &heights, decode_params_t &params,
                 FileNames &filenames)
��� : ���ڵ� �� �� ������ ���۸� ��ũ�� ��� ��
�Է� ������ : std::vector<nvjpegImage_t> &iout
             �ǹ� : ���ڵ� �Ϸ�� �� �������� ����
�Է� ������ : std::vector<int> &widths
             �ǹ� : ���ڵ� �Ϸ�� �� �������� ���� ȭ�� ũ�� ����
�Է� ������ : std::vector<int> &heights
             �ǹ� : ���ڵ� �Ϸ�� �� �������� ���� ȭ�� ũ�� ����



## Diagrams


And this will produce a flow chart:

```mermaid
graph LR
A[main start] --> B((readInput)) 
B --> C((process_images))
F-->C
E-->F{write_images}
C-->E{decode_images}
C --> D[main end]
```