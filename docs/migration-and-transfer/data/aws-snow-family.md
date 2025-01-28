# AWS Snow Family

AWS Snow Familyは、物理デバイスを使用してペタバイト規模のデータをAWSに移行するためのサービスです。

| デバイス | ストレージ容量 | メモリ(RAM) | vCPU | 特徴・用途 |
|---------|--------------|------------|------|------------|
| Snowcone | 8TB | 4GB | 2 | 約2kgの小型で堅牢なストレージ。 |
| Snowball Edge Storage Optimized (データ転送用) | 100TB（利用可能80TB） | 32GB | 24 | 大規模なデータ移行と定期的な転送ワークフロー、およびさらに高容量を必要とするローカルコンピューティングに適用 |
| Snowball Edge Storage Optimized | 210TB | 32GB | 24 | 大規模なデータ移行に対応（2023年5月追加） |
| Snowball Edge Compute Optimized | 42TB（利用可能39.5TB） | 416GB | 52または104基 | 機械学習、フルモーション動画分析、分析、ローカルコンピューティングスタックなどのユースケースに強力なコンピューティングリソースを提供 |
| Snowball Edge Compute Optimized (EC2搭載) | HDD 39.5TB<br>SSD 28TB | 512GB | 52 | EC2インスタンスを搭載したコンピュート最適化デバイス |
| Snowball Edge Compute Optimized with GPU | 80GB | 416GB | 52 (vCPU, GPU) | GPUを搭載したデバイス。機械学習や画像処理に最適 |
| Snowmobile | 100PB | - | - | 超大容量データをAWSに移動するために使用できるエクサバイト規模のデータ転送サービス |

各デバイスは、データ転送の規模や用途に応じて選択できます。Snowconeは小規模なデータ転送に、Snowball Edgeは中規模から大規模なデータ転送に、Snowmobileは超大規模なデータ転送に適しています。
