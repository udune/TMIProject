# 김민찬의 포트폴리오입니다

## TMI Project

안녕하세요. 김민찬 입니다.

이 프로젝트는 '악기를 연주고 녹음을 하는 방식으로 소리가 쌓이는 과정을 직접 느껴볼 수 있는'
악기 연주 콘텐츠를 만들어 본 프로젝트입니다.

> 사운드 옥타브 및 타입 변경
```c#
private string PathFinder(string soundName, int changeNum)
    {
        char slash = '/';

        foreach (SoundMenuData soundMenuData in SoundSystem.Instance.SoundMenu.SoundMenuData)
        {
            for (int i = 0; i < soundMenuData.instrumentSoundPath.Count; i++)
            {
                split = soundMenuData.instrumentSoundPath[i].Split(slash);

                if (split.Last() == soundName)
                {
                    changeIndex = OctaveMath(i, changeNum, soundMenuData.instrumentSoundPath.Count);
                    path = soundMenuData.instrumentSoundPath[changeIndex];
                }
            }
        }
        return path;
    }

    private int OctaveMath(int index, int changeNum, int count)
    {
        int reIndex = index + changeNum;

        if (reIndex < 0 || reIndex >= count)
        {
            Debug.Log("Octave is too lower or higher");
            return index;
        }

        return reIndex;
    }

    private AudioClip OctaveChange(string resourcePath)
    {
        AudioClip audioClip = null;

        audioClip = Resources.Load<AudioClip>(resourcePath);
        if (!audioClip)
        {
            Debug.LogError("Resources Load Error! FilePath = " + resourcePath);
            return null;
        }

        return audioClip;
    }
```
>   > soundManager를 통해 동적으로 생성된 500여개의 사운드를 dictionary로 담아
>   > 옥타브 변경 시 12단계를 기준으로 바뀌게 했고
>   > 타입 변경 시 리소스의 이름을 쪼개서 분별하는 식으로 작업했습니다.

