GQL

See example here: https://github.com/rambam613/gql/blob/master/example.ipynb
{
  "nbformat": 4,
  "nbformat_minor": 0,
  "metadata": {
    "colab": {
      "name": "gql_demo.ipynb",
      "provenance": []
    },
    "kernelspec": {
      "name": "python3",
      "display_name": "Python 3"
    }
  },
  "cells": [
    {
      "cell_type": "code",
      "metadata": {
        "id": "lZ5m1Q6NESQG",
        "colab_type": "code",
        "colab": {}
      },
      "source": [
        "!pip install pydrive\n",
        "!pip install pandasql\n",
        "!git clone https://github.com/rambam613/gql.git\n",
        "from gql import gql as gd\n",
        "import pandas as pd"
      ],
      "execution_count": 0,
      "outputs": []
    },
    {
      "cell_type": "code",
      "metadata": {
        "id": "FzTCHvu1EYrh",
        "colab_type": "code",
        "colab": {}
      },
      "source": [
        "#create a folder in google drive\n",
        "gd.create('gql_test')"
      ],
      "execution_count": 0,
      "outputs": []
    },
    {
      "cell_type": "code",
      "metadata": {
        "id": "vyLxeDJzEfTe",
        "colab_type": "code",
        "colab": {
          "base_uri": "https://localhost:8080/",
          "height": 34
        },
        "outputId": "ce3c3e9f-7936-4ae9-d785-f0a9e734590a"
      },
      "source": [
        "#list files in that folder\n",
        "gd.ls('gql_test')"
      ],
      "execution_count": 15,
      "outputs": [
        {
          "output_type": "execute_result",
          "data": {
            "text/plain": [
              "[]"
            ]
          },
          "metadata": {
            "tags": []
          },
          "execution_count": 15
        }
      ]
    },
    {
      "cell_type": "code",
      "metadata": {
        "id": "taqIX168EnjW",
        "colab_type": "code",
        "colab": {
          "base_uri": "https://localhost:8080/",
          "height": 195
        },
        "outputId": "1c3c4d2d-f4d1-41c1-b250-1ef55166a098"
      },
      "source": [
        "#read in data from the web\n",
        "df = pd.read_excel('https://www.eia.gov/dnav/ng/hist_xls/RNGWHHDd.xls',sheet_name=1,header=2)\n",
        "df.head()"
      ],
      "execution_count": 9,
      "outputs": [
        {
          "output_type": "execute_result",
          "data": {
            "text/html": [
              "<div>\n",
              "<style scoped>\n",
              "    .dataframe tbody tr th:only-of-type {\n",
              "        vertical-align: middle;\n",
              "    }\n",
              "\n",
              "    .dataframe tbody tr th {\n",
              "        vertical-align: top;\n",
              "    }\n",
              "\n",
              "    .dataframe thead th {\n",
              "        text-align: right;\n",
              "    }\n",
              "</style>\n",
              "<table border=\"1\" class=\"dataframe\">\n",
              "  <thead>\n",
              "    <tr style=\"text-align: right;\">\n",
              "      <th></th>\n",
              "      <th>Date</th>\n",
              "      <th>Henry Hub Natural Gas Spot Price (Dollars per Million Btu)</th>\n",
              "    </tr>\n",
              "  </thead>\n",
              "  <tbody>\n",
              "    <tr>\n",
              "      <th>0</th>\n",
              "      <td>1997-01-07</td>\n",
              "      <td>3.82</td>\n",
              "    </tr>\n",
              "    <tr>\n",
              "      <th>1</th>\n",
              "      <td>1997-01-08</td>\n",
              "      <td>3.80</td>\n",
              "    </tr>\n",
              "    <tr>\n",
              "      <th>2</th>\n",
              "      <td>1997-01-09</td>\n",
              "      <td>3.61</td>\n",
              "    </tr>\n",
              "    <tr>\n",
              "      <th>3</th>\n",
              "      <td>1997-01-10</td>\n",
              "      <td>3.92</td>\n",
              "    </tr>\n",
              "    <tr>\n",
              "      <th>4</th>\n",
              "      <td>1997-01-13</td>\n",
              "      <td>4.00</td>\n",
              "    </tr>\n",
              "  </tbody>\n",
              "</table>\n",
              "</div>"
            ],
            "text/plain": [
              "        Date  Henry Hub Natural Gas Spot Price (Dollars per Million Btu)\n",
              "0 1997-01-07                                               3.82         \n",
              "1 1997-01-08                                               3.80         \n",
              "2 1997-01-09                                               3.61         \n",
              "3 1997-01-10                                               3.92         \n",
              "4 1997-01-13                                               4.00         "
            ]
          },
          "metadata": {
            "tags": []
          },
          "execution_count": 9
        }
      ]
    },
    {
      "cell_type": "code",
      "metadata": {
        "id": "zP5sKICKE2JG",
        "colab_type": "code",
        "colab": {}
      },
      "source": [
        "#upload dataframe as csv (hh) to a folder (gql_test)\n",
        "gd.push(df,'gql_test/hh')"
      ],
      "execution_count": 0,
      "outputs": []
    },
    {
      "cell_type": "code",
      "metadata": {
        "id": "v58XNedIKM1v",
        "colab_type": "code",
        "colab": {
          "base_uri": "https://localhost:8080/",
          "height": 34
        },
        "outputId": "65c18c76-84d8-4ac3-d57e-040f50e0aa7f"
      },
      "source": [
        "#now check the list of files in the folder\n",
        "gd.ls('gql_test')"
      ],
      "execution_count": 19,
      "outputs": [
        {
          "output_type": "execute_result",
          "data": {
            "text/plain": [
              "['hh']"
            ]
          },
          "metadata": {
            "tags": []
          },
          "execution_count": 19
        }
      ]
    },
    {
      "cell_type": "code",
      "metadata": {
        "id": "dE6hHCG_E2wG",
        "colab_type": "code",
        "colab": {
          "base_uri": "https://localhost:8080/",
          "height": 195
        },
        "outputId": "474d36aa-6f0d-4fae-b97d-56713aa4ee3d"
      },
      "source": [
        "#read that csv to a dataframe\n",
        "gd.pull('gql_test/hh').head()"
      ],
      "execution_count": 18,
      "outputs": [
        {
          "output_type": "execute_result",
          "data": {
            "text/html": [
              "<div>\n",
              "<style scoped>\n",
              "    .dataframe tbody tr th:only-of-type {\n",
              "        vertical-align: middle;\n",
              "    }\n",
              "\n",
              "    .dataframe tbody tr th {\n",
              "        vertical-align: top;\n",
              "    }\n",
              "\n",
              "    .dataframe thead th {\n",
              "        text-align: right;\n",
              "    }\n",
              "</style>\n",
              "<table border=\"1\" class=\"dataframe\">\n",
              "  <thead>\n",
              "    <tr style=\"text-align: right;\">\n",
              "      <th></th>\n",
              "      <th>Date</th>\n",
              "      <th>Henry Hub Natural Gas Spot Price (Dollars per Million Btu)</th>\n",
              "    </tr>\n",
              "  </thead>\n",
              "  <tbody>\n",
              "    <tr>\n",
              "      <th>0</th>\n",
              "      <td>1997-01-07</td>\n",
              "      <td>3.82</td>\n",
              "    </tr>\n",
              "    <tr>\n",
              "      <th>1</th>\n",
              "      <td>1997-01-08</td>\n",
              "      <td>3.80</td>\n",
              "    </tr>\n",
              "    <tr>\n",
              "      <th>2</th>\n",
              "      <td>1997-01-09</td>\n",
              "      <td>3.61</td>\n",
              "    </tr>\n",
              "    <tr>\n",
              "      <th>3</th>\n",
              "      <td>1997-01-10</td>\n",
              "      <td>3.92</td>\n",
              "    </tr>\n",
              "    <tr>\n",
              "      <th>4</th>\n",
              "      <td>1997-01-13</td>\n",
              "      <td>4.00</td>\n",
              "    </tr>\n",
              "  </tbody>\n",
              "</table>\n",
              "</div>"
            ],
            "text/plain": [
              "         Date  Henry Hub Natural Gas Spot Price (Dollars per Million Btu)\n",
              "0  1997-01-07                                               3.82         \n",
              "1  1997-01-08                                               3.80         \n",
              "2  1997-01-09                                               3.61         \n",
              "3  1997-01-10                                               3.92         \n",
              "4  1997-01-13                                               4.00         "
            ]
          },
          "metadata": {
            "tags": []
          },
          "execution_count": 18
        }
      ]
    },
    {
      "cell_type": "code",
      "metadata": {
        "id": "248VJ8RWFJjl",
        "colab_type": "code",
        "colab": {}
      },
      "source": [
        "#delete the file\n",
        "gd.wipe('gql_test/hh')"
      ],
      "execution_count": 0,
      "outputs": []
    },
    {
      "cell_type": "code",
      "metadata": {
        "id": "LEFJ9I2wJoxg",
        "colab_type": "code",
        "colab": {}
      },
      "source": [
        ""
      ],
      "execution_count": 0,
      "outputs": []
    }
  ]
}
